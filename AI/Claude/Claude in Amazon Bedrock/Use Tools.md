The use of tools of Claude in Amazon Bedrock is really similar to the [[Tool Use]] it needs a [[JSON schema spec|JSON schema]] and follows the [[Tool Use Flow]], but here as Claude needs to runs through our backend calls there are few implementations in order to work:

## Stop and run a tool
Claude when noticed that it needs to use a tool it stops and return a text and more context with the information of the tools Claude wants to run:
![[Pasted image 20260818104621.png]]

as it could contain many tools to use we should handle the code to receive and execute these tools
```Python
def run_tool(tool_name, tool_input): 
	if tool_name == "get_current_datetime":
		return get_current_datetime(**tool_input)
	else:
		raise Exception(f"Unknown tool name: {tool_name}")

def run_tools(parts):
	tool_requests = [part for part in parts if "toolUse" in part] 
	tool_result_parts = []
	
	for tool_request in tool_requests:
		tool_use_id = tool_request["toolUse"]["toolUseId"]
		tool_name = tool_request["toolUse"]["name"]
		tool_input = tool_request["toolUse"]["input"]
		try:
			tool_output = run_tool(tool_name, tool_input)
			tool_result_part = {
				# This is the correct structure to return a tool result 
				"toolResult": {
					"toolUseId": tool_use_id,
					"content": [{"text": json.dumps(tool_output)}],
					"status": "success" }
				}
		except Exception as e:
			tool_result_part = {
				# Same structure but with error format
				"toolResult": {
					"toolUseId": tool_use_id,
					"content": [{"text": f"Error: {e}"}],
					"status": "error" }
				}
		tool_result_parts.append(tool_result_part)
	
	return tool_result_parts
```

Then we just simple have to pass the result of the request as a user to the chat  with the same array of tools and the history of the conversation.

## Structured data with tools
With any call of tools Claude needs to format the data in a specific order so the function gets what is needed to process, but maybe what we want is the actual structure of the data that Claude gives to the tool, anything else.
This is the idea behind this implementation. Make Claude to structure the data in certain way making him to think that he is making a call to a tool he needs to use.

![[Pasted image 20260818150322.png]]

## Batch tool use
Claude can natively run multiple tools at the same time, but some versions don't take advantage of this as much as you might wish. You can greatly increase the chances of Claude making multiple tool calls in a single message by implementing a batch tool.

Here's the basic structure of the batch tool specification:

```
{
  "name": "batch_tool",
  "description": "Invoke multiple other tool calls simultaneously",
  "input_schema": {
    "type": "object",
    "properties": {
      "invocations": {
        "type": "array",
        "description": "The tool calls to invoke",
        "items": {
          "type": "object",
          "properties": {
            "name": {
              "type": "string",
              "description": "The name of the tool to invoke"
            },
            "arguments": {
              "type": "string", 
              "description": "The arguments to the tool, encoded as a JSON string"
            }
          },
          "required": ["name", "arguments"]
        }
      }
    },
    "required": ["invocations"]
  }
}
```

The tool takes a list of invocations, where each invocation contains the name of a tool to call and its arguments (encoded as a JSON string).
### Implementation

The batch tool implementation involves two main functions:
 **The run_batch Function**

```
def run_batch(tool_input):
    batch_output = []
    for invocation in tool_input["invocations"]:
        tool_name = invocation["name"]
        args = json.loads(invocation["arguments"])
        
        tool_output = run_tool(tool_name, args)
        batch_output.append({"tool_name": tool_name, "output": tool_output})
    
    return batch_output
```

This function loops through each invocation, extracts the tool name and arguments, calls the appropriate tool using the existing `run_tool` function, and collects all the results.

**Adding to run_tool**

You also need to add a case to your main `run_tool` function:

```
elif tool_name == "batch_tool":
    return run_batch(tool_input)
```

Note that unlike other tools, you pass `tool_input` directly without using the splat operator (`**`), since the batch tool needs to handle the raw input structure.

## Text editor Tool
The Text Editor Tool is Claude's built-in capability that gives it file system access and text editing abilities. Unlike other tools where you write both the schema and implementation, Claude already knows how to request text editor operations - you just need to handle those requests.

## What the Text Editor Tool Does

This tool gives Claude the ability to work with files and directories like a software engineer would:

- View file or directory contents
- View specific ranges of lines in a file
- Replace text in files
- Create new files
- Insert text at specific line numbers
- Undo recent edits
The Text Editor Tool is different from custom tools because only the JSON schema is built into Claude. You still need to provide the actual implementation.

### Setting Up the Tool

To use the Text Editor Tool, you need to provide specific tool names that vary by Claude version:

```
# For Claude 3.7
text_editor = "text_editor_20250124"

# For Claude 3.5  
text_editor = "text_editor_20241022"
```

You'll also need to modify your chat function to accept the text editor parameter and include it in the model configuration.