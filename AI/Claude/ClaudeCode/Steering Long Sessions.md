## Scope
Scope the work first with plan mode, before Claude writes a single line of code, get it to lay out a plan. In plan mode, Claude does its research in read-only mode. It reads the code, figures out what needs to change, and hands you a plan to review.

When you get that plan, actually read it. Don't skim it. Te more thorough the plan, the fewer surprises you'll hit once Claude starts executing. If something's off or missing, just ask Claude to add it where you want. Iterating on a plan is much faster than letting Claude run and hoping for the best, then cleaning up the mess.

## Useful commands
**Compact**: For log sessions the context window starts to become a problem, for that we have the 
```code
/compact
```
command, but this will probably make we loose some context we don't want, so for that we can add it more context of what we want it to focus on:
```code
/compact Focus on the --version flag implentation
```

**Rewind:** When Claude goes down the wrong path, you don't have to prmpt your way out of it the rewind command help us to go back to the last check. Every user prompt creates a checkpoint that you can revert back to with different options:

- Restore code and conversation
- Restore conversation
- Restore code
- Summarize from here (Will summarize everything after the checkpoint)
- Summarize up to here (Will summarize everything before the checkpoint)
```code
/rewind
```

**/goal and /loop:** When we talk about steering, we assume that we are hands-on, but if we want something a little bit more autonomous, there is the goal and loop.

- **Goal**: Goal sets a completion condition. You describe what "done" looks like, and Claude keeps working across turns until a fast evaluator confirms those conditions are met. It won't just stop the first time it thinks it's finished.
  ```code
  /goal all tests in src/billing pass, and the type checker reports zero errors
  ```
  To cancel it, run `/goal clear`. One important constraint: the evaluator only reads the transcript. So your condition has to be checkable from the output Claude actually produces, like the results of a test run.
- **Loop:** Loop runs a prompt on an interval between turns, either fixed or self-paced. Use it to pull something external, like a CI run or a deploy, and act when the state changes. To stop a loop, just press escape.
  ```code
  /loop
  ```
## Run parallel work with worktrees
Instead of sessions stepping on each other, each one gets its own independent file tree.

Because each agent has its own tree, they can't clobber each other's changes. When a session exits, a clean worktree is automatically removed.

There's one helpful file to know about. A `.worktreeinclude` file at the repo root lists git-ignored files to copy into each worktree. This is useful for things like an environment variable file or a local config that you need in every worktree but don't want to commit to version control.