The hierarchical decomposition pattern builds a goal tree: goals break into sub-goals, sub-goals into tasks

A **Top-level orchestrator** holds the overall goal and delegates subgoals. Each sub-goal is managed by an LLM that handles only its tier of complexity, depending the complexity the agent generates tasks that will be performed by another

>[!Note]
>It is like see how human organizations delegate work across management layers.

![[Pasted image 20260909162723.png]]

## When to go Deep vs Flatten
hierarchy depth is a design choice - deeper trees enable specialization but increase coordination overhead. Take into account that a Flatten hierarchies is better wherever possible, just try to not loose the benefits os specialization.

**Go deeper** When subtasks require fundamentally different capabilities (Each added level increases error propagation surface)
**Go Flatten** When subtasks are similar enough to share one agent

