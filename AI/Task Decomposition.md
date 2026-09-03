Task decomposition determines how complex work is broken into manageable units. The right strategy depends on whether the workflow is predictable or open-ended.

#### Attention Dilution

Large inputs (e.g., reviewing a 50-file PR in one pass) cause attention dilution -- the model may miss issues in the middle of long contexts. The solution is decomposition:

1. Per-file local analysis (each file gets focused attention)
2. Cross-file integration pass (finds interactions between files)

This two-pass approach catches both local issues and cross-cutting concerns.

Choosing between fixed and adaptive decomposition is a critical architectural decision that affects both quality and efficiency.

### Fixed Sequential Pipelines (Prompt Chaining)

Best for predictable, multi-aspect workflows:

- Analyze each file individually, then run a cross-file integration pass
- Break reviews into sequential steps with defined inputs/outputs
- Each step's output feeds the next step's input

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