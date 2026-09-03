Model Context Protocol (MCP) is an open standard and a communication layer that lets an agent connect to external tools and data sources. It connects with context and tools without requiring you to write a bunch of tedious integration code. Think of it as a way to shift the burden of tool definitions and execution away from your server to specialized MCP servers

![[Pasted image 20260827114545.png]]

There are 2 main types of MCPs:
- **http:** Those are for remote services and hosted by the service provider and connected through the network
- **stdio**: These are for local process that lives in the machine

They can live local (For the current project), User (shared across all the projects of the user), Project that can be shared through all the devs of a project (For claudeCode use .mcp.json).

The MCPs loads all the tools into the context, Be careful with the context window!
