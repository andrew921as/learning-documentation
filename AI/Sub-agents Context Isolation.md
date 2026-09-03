Subagents do NOT automatically inherit parent context or share memory between invocations. All necessary context must be explicitly provided in the subagent's prompt. This means:

- Pass complete findings from prior agents directly in the prompt
- Use structured data formats to separate content from metadata (URLs, document names, page numbers) for attribution
- Don't assume the subagent knows anything not in its prompt

The great advantage of it is that it helps to keep the main context clean, with only valid information while the sub-agent has its context isolated it also makes sure the sub-agent do not reach either the context window limit