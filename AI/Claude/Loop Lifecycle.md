cAgents iterates responses and re-think what they are doing based on different inputs during the reasoning process, to this re-think we called **Loop Lifecycle** and is simply recall the LLM with more context.

The agent ([[ClaudeCode]]) bases itself in 4 different fases Explore -> Plan -> Code-> Commit Workflow
To be effective with [[ClaudeCode]], follow the Explore, Plan, Code, and Commit workflow:

- **Explore** gives Claude the relevant context it needs for your project.
- **Pla[[Agent SDK Hooks]]n** creates a plan of action that Claude uses to measure success.
- **Code** is the back and forth between you and Claude before settling on the final outcome.
- **Commit** helps you review and push your code so you can start on your next feature.

![[Pasted image 20260811225006.png]]

#### The Loop

```
while True:
    response = call_claude(messages)
    
    if response.stop_reason == 'end_turn':
        break  # Task complete
    
    if response.stop_reason == 'tool_use':
        results = execute_tools(response.tool_calls)
        messages.append(response)
        messages.append(tool_results(results))
```

### The stop_reason
There is a stop_reason returned by the agent during each call, and depending of the stop_reason we can decide what to do:
#### Stop Reason Values

| Value           | Meaning                                  | Action                                                 |
| --------------- | ---------------------------------------- | ------------------------------------------------------ |
| `end_turn`      | Claude finished its response naturally   | Present response to user                               |
| `max_tokens`    | Hit the max_tokens limit                 | Response may be truncated; consider increasing limit   |
| `stop_sequence` | Hit a custom stop sequence               | Parse response up to the stop sequence                 |
| `tool_use`      | Claude wants to use a [[Tool Use\|tool]] | [[Tool Use Flow\|Execute the tool]] and return results |
It is recomendable to set a maximum iteration safety guardrail as a backup, so the agent do not iterate for ever and lose the main context.
