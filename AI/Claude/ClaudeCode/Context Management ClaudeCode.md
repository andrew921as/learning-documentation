Context is Claude's working memory. Every file it reads, every command it runs, every message you send — it all takes up space in the context window.

to see the context used in any session of Claude Code type:
```
/context
```
in the ClaudeCode terminal CLI

## Context Window
Whenever you enter a prompt, Claude reads a file, runs a tool call, or receives a tool call result, it's all adding to the context window.

When the context window is reaching the limit ClaudeCode automatically compacts it. It will summarize important details and removes the API results that are not longer necessary (This could cause loose of information during the session).

To compact the context manually just run the command:
```
/compact
```

To remove the context the Claude Code has just run the command:
```
/clear
```

## Tips to not consume too much context
The main tip is to be specific, if I tell where do I want the change, and how is better to keep a low context window. At first glance you are giving the tool more text and things to process on, but the text you write is shorter than the tool consuming all the files and adding them to the context to find the place where the implementation should be done, or looking for possible options on internet.

Also disable the MCP's servers running that are not usefull for this task. The MCP loads all the tools to the context, instead use Skills if able; the skills only loads the description 'header' of them to the context.

Use sub agents, maybe a task can be delivered using a sub-agent and only a resume or result of the task is needed to continue working. In that way the main Agent only loads the necessary information to the context.
