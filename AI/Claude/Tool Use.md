Tools allow Claude to access information from the outside world, solving one of its key limitations. By default, Claude only has access to information it was trained on, which means it can't provide current information like today's weather or recent news.
Tools fix this problem by creating a bridge between Claude and external data sources.
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

## Text Editor Tool:
The Text Editor Tool is Claude's built-in capability that gives it file system access and text editing abilities. Unlike other tools where you write both the schema and implementation, Claude already knows how to request text editor operations - you just need to handle those requests.
It means we don't have to create any tool so this works
