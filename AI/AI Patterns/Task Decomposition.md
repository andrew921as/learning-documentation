Task decomposition determines how complex work is broken into manageable units. The right strategy depends on whether the workflow is predictable or open-ended.

#### Attention Dilution

Large inputs (e.g., reviewing a 50-file PR in one pass) cause attention dilution -- the model may miss issues in the middle of long contexts. The solution is decomposition:

1. Per-file local analysis (each file gets focused attention)
2. Cross-file integration pass (finds interactions between files)

This two-pass approach catches both local issues and cross-cutting concerns.

Choosing between fixed and adaptive decomposition is a critical architectural decision that affects both quality and efficiency.

### Fixed Sequential Pipelines (Prompt Chaining)

Best for predictable, multi-aspect [[Workflow|workflows]]:

- Analyze each file individually, then run a cross-file integration pass ([[Parallel Decomposition-Execution| Parallel Execution]])
- Break reviews into sequential steps with defined inputs/outputs
- Each step's output feeds the next step's input ([[Sequential Execution-Decomposition|Sequential Execution]])

Example: Split large code reviews into per-file local analysis passes plus a separate cross-file integration pass to avoid attention dilution.
#### When to Use Fixed Pipelines

- The workflow has well-defined stages (e.g., extract -> validate -> transform -> load)
- Each stage has predictable inputs and outputs
- The number of steps is known in advance
- Quality comes from thoroughness at each stage, not exploration

### Dynamic Adaptive Decomposition

Best for open-ended investigation tasks:

- Generate subtasks based on what is discovered at each step
- First map structure, identify high-impact areas, then create a prioritized plan
- Plan adapts as dependencies are discovered

Example: "Add comprehensive tests to a legacy codebase" -- first map the codebase structure, identify high-impact untested areas, then create a test plan that adapts as you discover dependencies.

#### When to Use Adaptive Decomposition

- The scope is unknown until investigation begins
- Early findings change what needs to be investigated next
- Dependencies between subtasks are discovered during execution
- The task requires exploration before planning
## Handoff Message
A structured payload with task, context, output format, and constraints the receiver needs. It has 4 main components:

 - **Task description**: What the receiver is asked to produce
 - **Relevant context**: Only the facts the receiver needs
 - **Output format**: Exactly what structure the result takes
 - **Constraints**: Boundaries, scope limits, safety restrictions
 
```json
{
	"task":"...",
	"context":[..],
	"format":{..},
	"constraints":[..]
}
```

It should **Include** what the receiver needs to act without the sender's context: task, relevant facts, output format, and explicit constraints.
Also it should **Avoid** the full conversation history, internal deliberation, sender state, and redundant context. Other thing to keep in mind is that these schemas shouldn't say which agent runs or continue, they should be agnostic to the agent

>[!important]
>Each handoff schema should be versioned, they should evolve without breaking anything in the process

The Sender need verification that the receiver got the task complete and everything is good to proceed, this avoids that the sender ends it's process with an invalid output. To achieve that the tasks should have checkpoints, it means save the task state before initiating any handoff. In case of any failure the  task should start from the last **confirmed good checkpoint** NOT just from the last. Finally the Retry should resumes from the checkpoint and not from the beginning.

![[Pasted image 20260913180042.png]]