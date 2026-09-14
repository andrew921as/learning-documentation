Parallel decomposition finds independent pieces of work with no data dependencies and runs them concurrently to save time. It is important to notice that each parallel branch must be truly independent between them. they should only depend from the last task.

## Fan-Out
The step where a single task splits into multiple concurrent subtasks dispatched simultaneously.
This is in charge to dispatch all branches at the same time from this single control point.

>[!Note]
>Notice that branches can be agents, tool calls, or sub-workflows - not just simple functions

**Hint** to make calls to multiple tool calls with Claude you can use a [[Use Tools#Batch tool use|Batch tool use]]
## Fan-In
It is a step that collects all branch results before continuing with the execution. it allows mergins all the information. It also handles **partial failure:** Some branches succeed, others fail; This scenario requires explicit handling.

![[Pasted image 20260913103551.png]]
in the image the **Fan-in** will be the last box (Best U,WWR,Wall and Roof...).

### Partial Failure Handling
When some branches succesd and others fail, the fan-in step has to decide what to do:

- **Fain The Pipeline**: Any branch failure aborts the whole operation.
- **Proceed with partial results**: Continues with what succeeded, flag what failed.
- **Retry Failed Branches**: Re-dispatch individual branches that returned errors.
### Result Mergin Strategies:
How fan-in aggregates the branch results depends on the pipeline's purpose and output type:
- **Voting**: Multiple branches answer the same question: Majority result wins
- **Concatenation:** Outputs from independent branches are joined into one list.
- **Structured Aggregation:** Each branch contributes a named field to a shared object.