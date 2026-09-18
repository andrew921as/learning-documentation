 The schema has two main parts: the name and description at the top (which help Claude understand when to use the tool), and the actual schema that describes the function's arguments.
 ![[Pasted image 20260818084530.png]]

There are tons of tools online that helps to build a JSON schema, so we can use it.

We just simply past the JSON of our arguments with examples to one of the converters like *JSON to JSON schema* in internet and it will return an example of the schema for the function, at least of the inputSchems.

![[Pasted image 20260818085732.png]]

Then we just need to add it to the whole schema of the function in the section of 
```json
'toolSpec':{
	'name':"descriptive_function_name"
	'description':"",
	'inputSchems'{
		'json':{
			... //The generated code goes here
		}
	}
}
```

**Best practices:**
- [[Tool Design Interface|Explain what the tool does, when to use it and what it returns]]
- Aim for 3 to 4 sentences
- Provide super detailed descriptions
![[Pasted image 20260818085013.png]]

## Strict tool use
 Forcing a tool call is only half the battle; setting strict to true guarantees the model's tool inputs match your schema
 Setting `strict: true` on a tool definition guarantees Claude's tool inputs match your JSON Schema by constraining the model's token sampling to schema-valid outputs (a technique called grammar-constrained sampling).
 Building reliable agentic systems requires guaranteed schema conformance. Without strict mode, Claude might return incompatible types (`"2"` instead of `2`) or omit required fields, breaking your functions and causing runtime errors.

Strict tool use guarantees type-safe parameters:

- Functions receive correctly-typed arguments every time
- No need to validate and retry tool calls
- Production-ready agents that work consistently at scale

```Python
client = anthropic.Anthropic()

response = client.messages.create(
    model="claude-opus-5",
    max_tokens=1024,
    messages=[{"role": "user", "content": "What's the weather like in San Francisco?"}],
    tools=[
        {
            "name": "get_weather",
            "description": "Get the current weather in a given location",
            "strict": True,  # Enable strict mode
            "input_schema": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                        "description": "The city and state, e.g. San Francisco, CA",
                    },
                    "unit": {
                        "type": "string",
                        "enum": ["celsius", "fahrenheit"],
                        "description": "The unit of temperature, either 'celsius' or 'fahrenheit'",
                    },
                },
                "required": ["location"],
                "additionalProperties": False,
            },
        }
    ],
)
print(response.content)
```

What the Agent calls:
```JSON
{
  "type": "tool_use",
  "name": "get_weather",
  "input": {
    "location": "San Francisco, CA"
  }
}
```
