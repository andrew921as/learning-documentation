Sequential decomposition creates a dependency chain where each step's output becomes the next step's input. Sequential patters are appropriate whenever genuine data dependencies exist between steps.

The step order is enforced because downstream steps need upstream output. Those are easier to reason about and debug than parallel workflows.

Any failed step halts the chain until it's resolved.

![[Pasted image 20260913103022.png]]


## When to use Sequential?
There are 4 main scenarios where use a sequential architecture is the right choice:
- **Data Dependency**: Step B cannot start until step A finishes. The two cannot run at once.
- **State Accumulation:** Each step builds on context that earlier steps produced.
- **Ordered Transforms**: Operations run in a strict order, one stage at a time.
	- **Simplicity Goal:** Debugging and auditability matter more than raw speed.`