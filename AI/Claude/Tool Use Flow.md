Tool use in the Claude API follows a structured request-response cycle that your application must implement.

#### The Tool Use Cycle

- **Define tools**: Provide tool definitions in the API request
- **Claude selects a tool**: Response includes `tool_use` content block with tool name and input
- **Execute the tool**: Your application runs the actual tool/function
- **Return results**: Send tool results back to Claude in a `tool_result` content block
- **Claude continues**: Uses the results to generate its response or call more tools

#### Response Structure

When Claude wants to use a tool, the response contains:

- `stop_reason: "tool_use"`
- Content blocks of type `tool_use `with` name`,` id`, and` input`

It is important to notice that the Agent will **STOP** the conversation to use a tool, in order to continue with the chat or any other implementation it is needed to catch the stop_reason, execute the tool and then send the result of the tool to continue the execution.
The SDK make this by default but other implementations like [[How to make requests|Claude in Amazon Bedronck]] needs a further implementations in the backend to manage these kind of requests.

#### Model-Driven vs Pre-Configured

The distinction matters for architecture:

- **Model-driven**: Claude reasons about which tool to call next based on context. More flexible, adapts to novel situations.
- **Pre-configured**: Fixed decision trees or tool sequences defined in code. More predictable, but less adaptable.

#### Parallel Tool Use

Claude can request multiple tools in a single turn. Return all tool results together before the next API call to minimize round-trips.