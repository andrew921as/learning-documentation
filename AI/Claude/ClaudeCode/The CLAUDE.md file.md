One of the most useful features in Claude Code is the CLAUDE.md file. It gives Claude Code persistent memory about your project.

When you open Claude Code without a CLAUDE.md file, it starts fresh every time. CLAUDE.md solves this. It's a Markdown file you add to the root of your project, and Claude Code reads it automatically every time you start a session. Think of it as an onboarding script for your codebase. The contents of the CLAUDE.md file are appended to your prompt.

To generate an automated Claude.md file execute the next command in ClaudeCode:
```
/init
```
This will generate an automated Claude.md file based on the project.

The recommendation is to start a project without a CLAUDE.md file, this is because with the init command makes sure that Claude creates the file with the info it actually needs.

Be careful to not fill the CLAUDE.md file with a bunch of technical aspects. For example how to create a new React component; It should be a [[Skills|skill]]!

## Where does the CLAUDE.md file lives?
There are 4 main parts where does the `CLAUDE.md` file lives:
- Managed policy: The org-level file your platform team controls
- User file: Your personal preferences across every project on your machine
- Project file: shared with your team
- Local: Ignored by git. Your personal notes for this repository only
## How to keep it short?
Split up a big file with imports When your project file starts getting long, you can break it into pieces using the path-to-file import syntax. Instead of one wall of text, you point to other files:

```
@.claude/conventions/code-style.md
@.claude/conventions/testing.md
@.claude/conventions/workflow.md
```

This is great for organizing. But know exactly what it buys you, because it's easy to get the wrong idea. When Claude launches, it expands those imported files inline, right where you referenced them. So imports help you keep things tidy, but everything still loads up front. They do not reduce the amount of context Claude has to read. Use imports to organize, not to shrink the load.

## Be positive
Instead of saying *Do not do this or that* if is there a positive way of saying is much better for the context, in some point Claude can miss the NOT and use whatever you wanted it to avoid.

