Subagents in the Agent SDK are spawned using the `Task` tool. The coordinator must be configured with `allowedTools` that includes `"Task"` to invoke subagents. Remember that usually for the Orchestrator patter the sub-agents should have their [[Sub-agents Context Isolation||context isolated]]. 

### Key Mechanics

- **Task tool**: The mechanism for spawning subagents. Each `Task` tool call creates an independent subagent execution.
- **allowedTools**: The coordinator's tool list must include `"Task"` or it cannot delegate work. (also Agent or runSubagent are allowed in other models)
- **AgentDefinition**: Configures each subagent type with descriptions, system prompts, and tool restrictions.

#### Parallel Spawning

Spawn parallel subagents by emitting multiple `Task` tool calls in a single coordinator response rather than across separate turns. This is analogous to Claude's parallel tool use -- multiple tasks in one response minimizes round-trips.

#### Coordinator Prompt Design

Specify research goals and quality criteria rather than step-by-step procedural instructions. This enables subagent adaptability -- the subagent can decide HOW to achieve the goal rather than rigidly following prescribed steps.