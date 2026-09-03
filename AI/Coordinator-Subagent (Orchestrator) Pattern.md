The coordinator (orchestrator) pattern uses a central agent to manage specialized subagents, maintaining control over task decomposition, routing, and result aggregation.

## Coordinator Agent
The coordinator agent should only [[Sub-agent Invocation||create new agents]] to each task of a problem, never think by itself the solution, only divide the problem in tasks, as an example, the coordinator agent should create the next agents to generate a report:

- Web Search Agent
- Document Analysis Agent
- Synthesis Agent
- Report Generation Agent

### Key Principles:
All inter-agents communication flows through the coordinator:
Sub-agents **NEVER** communicate directly with each other. They operate with [[Sub-agents Context Isolation||isolated context]], it means that they do not inherit the coordinator's conversation history.
Coordinator observes all interactions, as it handles erres consistently, finally the coordinator decides what information each subagent receives.

All of these principles receives the name of **Hub-and-Spoke Communication**

### Iterative Refinement
The coordinator evaluates synthesis output for gaps, re-delegates to subagents with targeted queries, and re-invokes synthesis until coverage is sufficient.

### Benefits:
1. Centralized visibility: The coordinator manage all interactions
2. Consistent error handling: There will be one place for recovery logic and manage errors
3. Information control: The data of each agent do no get *"dirty"* by any other result of other agents
4. Flexible routing: Change downstream agents without affecting upstream.

## Narrow Decomposition Risk
When a coordinator agent decomposes a broad topic into subtasks, narrow decomposition is a common failure mode that produces incomplete results.

### Example:
Topic: "Impact of AI on creative industries"
Coordinator decomposes into:
- AI in digital art creation
- AI in graphic design
- AI in photography

Result: Report covers only visual arts, completely missing music, writing, and film.
The coordinator's task decomposition was too narrow. All three subtasks focused on visual arts, missing other creative domains.
#### Solutions

- **Explicit decomposition guidelines**: "Ensure subtasks cover ALL relevant sub-domains"
- **Coverage validation**: After decomposition, validate that subtasks span the full scope
- **Domain enumeration**: Require the coordinator to enumerate all relevant domains before creating subtasks
- **Partition by source type**: Assign distinct subtopics or source types to each agent to minimize duplication
#### Diagnostic

When subagents all succeed but the final output has gaps, the root cause is usually the coordinator's decomposition, not the subagents' execution.