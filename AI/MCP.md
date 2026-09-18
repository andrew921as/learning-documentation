Model Context Protocol (MCP) is an open standard and a communication layer that lets an agent connect to external tools and data sources. It connects with context and tools without requiring you to write a bunch of tedious integration code. Think of it as a way to shift the burden of tool definitions and execution away from your server to specialized MCP servers

![[Pasted image 20260827114545.png]]

There are 2 main types of MCPs:
- **http:** Those are for remote services and hosted by the service provider and connected through the network
- **stdio**: These are for local process that lives in the machine

They can live local (For the current project), User (shared across all the projects of the user), Project that can be shared through all the devs of a project (For claudeCode use .mcp.json).

>[!Warning]
> The MCPs loads all the tools into the context, Be careful with the context window!

## STDIO Transport
The **stdio transport** is a local communication method in the **Model Context** Protocol where a client launches a server as a subprocess and exchanges data through standard input (`stdin`) and standard output (`stdout`).

In the STDIO transport the client is the parent of a process and the server is the child.

This works making that the client spawns the server binary as a child process at startup, this means only the tool/server needed to run the task is deployed and running, all MCP messages flow over stdin and stdout as newline-delimited JSON. When the client process finished the server is killed.

It is the standard for ClaudeCode local MCP's

>[!important]
>This method works only for local MCP's when the client and server works in different machines there are SSE or streamable HTTP (this is the standard nowadays)
