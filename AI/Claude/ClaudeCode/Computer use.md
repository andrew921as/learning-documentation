Computer use in Claude works exactly like regular tool use - it's built on the same foundation you're already familiar with. The key difference is that instead of calling a weather API or database function, Claude is making requests to control a computer interface.

![[Pasted image 20260821110204.png]]

Here's the typical flow:

1. You send Claude a question along with available tool schemas
2. Claude analyzes the request and decides it needs to use a tool
3. Claude responds with a tool use request containing the tool name and required inputs
4. Your server executes the tool function and returns the result
5. You send the tool result back to Claude

### Computer Use: Same Flow, Different Tool

Computer use follows this exact same pattern. The difference is in what the "tool" actually does - instead of fetching weather data, it simulates computer interactions like mouse clicks and keyboard input.
When you enable computer use, you send Claude a special tool schema that gets automatically expanded behind the scenes. What starts as a simple schema on your end becomes a comprehensive interface that tells Claude it can perform actions like:

- Mouse movements and clicks
- Keyboard input and key combinations
- Taking screenshots
- Scrolling and other interface interactions