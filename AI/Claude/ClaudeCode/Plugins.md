A plugin is one installable unit. It bundles everything you'd otherwise share by hand: skills, subagents, hooks, and MCP server configs, plus the longer tail of stuff like language server protocol servers, background monitors, themes, and a slice of `settings.json`. One version, one install.

Where the plugin lives decides how you install it. Inside a session, you can install one directly by name:

```
/plugin install org-name@plugin-name
```

Here's what that looks like. Claude Code installs it and tells you to run `/reload-plugins` to apply the change.

## Adding a marketplace for your team

For a team, the better move is to add a private marketplace once. A marketplace is a shared source that plugins resolve through:

```
/plugin marketplace add your-org/claude-plugins
```

Call it whatever you want. Once it's added, every install after that resolves through it. You get centralized discovery, version tracking, and updates in one place instead of scattered across everyone's laptop.

You can browse what's available from the Discover tab. It lists the plugins on your marketplaces so you can search and pick.

## Read before you install

Here's the part that matters most. A plugin runs code on your machine, with your privileges. Its hooks fire on every matching tool call. So if you install a plugin for its skills, you also get its PreToolUse and Stop hooks whether you read them or not.

## Components run alongside yours

A plugin doesn't overwrite your configuration. Its components run alongside your own. That's mostly good, but it has consequences you should understand.

Hooks stack. A plugin's PreToolUse hook and your own PreToolUse hook both fire on every tool call. Neither replaces the other. This is exactly why you read the details first.

Skills, agents, and commands are namespaced under the plugin name, so they never clash with yours. A plugin can also ship a `settings.json` file, but only a narrow one. Claude Code honors just two keys from it: the agent and subagent status line keys.

That agent key is worth a pause. Setting it promotes one of the plugin's subagents to the main thread, along with its system prompt, tool restrictions, and model. In other words, enabling the plugin can change how Claude Code behaves by default. That's one of the main reasons to look before you even turn it on.

Once a plugin is installed you can see everything it added, manage it, and uninstall it from the plugin panel.

## Packaging your own plugin

Now the other side. Once you've built a `.claude` directory that works, don't make your team copy and paste it between machines. Package it instead.

The good news is you don't have to restructure anything. A plugin uses the same `.claude` shape you already use:

- One folder per skill.
- One markdown file per subagent under `agents`.
- `hooks/hooks.json` and `.mcp.json`, at the plugin root.

The directory structure does most of the work. Claude Code discovers components by convention.

## The manifest

On top of that, there's an optional manifest. It lives at `.claude-plugin/plugin.json` and holds the name, version, description, and author:

```
{
  "name": "svg-splitter-review",
  "version": "0.1.0",
  "description": "Reviews the SVG Splitter repo",
  "author": {
    "name": "Lewis Menelaws"
  }
}
```

The manifest is optional. Leave it out and Claude Code still discovers your components by directory convention. But a couple of details are worth knowing:

- **Name is the only required field.** It namespaces your skills as `company-name:skill-name`, which keeps them from colliding with anyone else's.
- **Version it like any other dependency.** That's what makes updates and version tracking work across your team.