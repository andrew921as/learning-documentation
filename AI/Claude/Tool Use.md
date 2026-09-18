  Tools allow Claude to access information from the outside world, solving one of its key limitations. By default, Claude only has access to information it was trained on, which means it can't provide current information like today's weather or recent news.
Tools fix this problem by creating a bridge between Claude and external data sources.

see more of how to create a tool and what a batch tool is at: see more at [[Use Tools]]

The tool use process follows a specific [[Tool Use Flow|flow]] that involves multiple back-and-forth communications between your server or code and Claude:
![[Pasted image 20260818083251.png]]

In practice, you often need to:

- Write the tool function first
- Create a [[JSON schema spec|JSON schema specification]]
- Handle the ToolUse and ToolResult parts
- Include the schema with your request

## Writing a tool function
To write a tool function is recomendable to write the function in a language like Python or JS and those are plain functions that get executed when Claude decides it needs additional information to help the user. Here's how to write them effectively:

### Best Practices

- **Use well-named**, descriptive arguments (this becomes important later)
- **Validate the inputs**, raising an error if they fail validation
- **Return meaningful errors** - Claude will try to call your function a second time if it gets an error

### Designing Error Messages for Claude
The error messages of a tool should be concise and tell only what a model needs to know to continue it processing.

A error response or even success has this schema:
- **tool_use_id**: matches the result back to the originating call
- **content**: The result text, or an error message when it failed
- **is_error**: set true to flag that execution failed

>[!important]
>Any message for the agent should be in the content, the agent wont read any other parameter than these 3 described above.

A suggestion of a content for an error is to keep codes stable across versions so logic doesn't break, also you could include the input value that triggered the error and finally **Avoid** raw stack traces as the primary message(It only create noise and should be kept for a logging system)
### Text Editor Tool:
The Text Editor Tool is Claude's built-in capability that gives it file system access and text editing abilities. Unlike other tools where you write both the schema and implementation, Claude already knows how to request text editor operations - you just need to handle those requests.
It means we don't have to create any tool so this works.




