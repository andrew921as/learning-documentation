Long-running agent work often spans multiple sessions. Managing session state correctly prevents wasted work and stale context issues.
#### Named Session Resumption
Use `--resume <session-name>` to continue a specific prior conversation. This preserves the full conversation history including tool results from the previous session.

### When to Resume vs Start Fresh

| Scenario                                    | Strategy                                    |
| ------------------------------------------- | ------------------------------------------- |
| Prior context is mostly valid               | Resume with `--resume`                      |
| Files have been modified since last session | Resume but inform agent of specific changes |
| Prior tool results are stale (data changed) | Start fresh with structured summary         |
| Exploring a different approach              | Fork the session                            |
#### Targeted Re-Analysis

When resuming after code modifications, inform the agent about specific file changes rather than requiring full re-exploration. This enables targeted re-analysis of only what changed.

#### fork_session

Create independent branches from a shared analysis baseline to explore divergent approaches:

- Compare two testing strategies from a shared codebase analysis
- Try different refactoring approaches without losing the original analysis
- Each fork operates independently with its own conversation history