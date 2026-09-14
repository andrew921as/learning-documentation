As is development there are different patters to work with AI agents as long as they can manage different tasks at a time. Notice that not all the patters comes only on the AI context and can be applied to several automatizations or even code.

Here we have to make a special mention to the [[Workflow|Workflows]], as they are not by themselves a patters they have different patters that the AI can use to work and interact.

Most of the patters comes with a question how to decompose a task? when to? and tools that help us to chain the answers the agents give to us. See [[Task Decomposition]] for more information.

## Decomposition Patters
These are patters that a single task or goal is divided in to several other tasks by different agents.
- **[[Hierarchical Decomposition]]:** Split goals into sub-goals across multiple levels, creating a tree structure where orchestrators delegate down; and results flow back up
- **[[Sequential Execution-Decomposition|Sequential Execution]]:** Tasks performed in order, where each step may depend on the previous step's output before proceeding.
- **[[Parallel Decomposition-Execution|Parallel Execution]]:** Independent subtasks run concurrently, reducing total runtime. Requires a synchronization point to collect results.

## Dynamic planning & Static planning

- **[[Coordinator-Subagent (Orchestrator) Pattern|Coordinator-Subagent]]**: The coordinator pattern uses a central agent to manage specialized subagents.
- 