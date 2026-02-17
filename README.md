# Skills

A collection of AI agent skills and Claude Code plugins for development workflows.

## Available Skills

### react-vite-kitchen-sink

Scaffold fully-configured React+Vite projects with Tailwind, React Query, Router, Vitest, and Axios. Also provides contextual guidance when working in projects built with this stack.

**Slash command:** `/kitchensink:scaffold [project-name]`
**Auto-skill:** Activates when working in React+Vite projects with the kitchen sink stack

#### What's in the stack

- React 18 + TypeScript + Vite
- Tailwind CSS (via Vite plugin)
- @tanstack/react-query
- React Router
- Axios + qs
- Zod
- Vitest + Testing Library

## Installation

### Claude Code Plugin

Add to `~/.claude/settings.json`:

```json
{
  "enabledPlugins": {
    "react-vite-kitchen-sink@react-vite-kitchen-sink": true
  }
}
```

Or use `/plugins` within Claude Code to install from the local path.

### Other AI Agents

Each skill's source repo includes an `AGENTS.md` at the root. Any agent that supports the AGENTS.md convention (Claude Code, Codex, Cursor, etc.) will pick it up automatically when working in that repo.

## Structure

```
skills/
└── <skill-name>/
    ├── .claude-plugin/
    │   └── plugin.json          # Plugin metadata
    ├── commands/
    │   └── <namespace>/
    │       └── command.md       # Slash commands (user-invoked)
    └── skills/
        └── <skill-name>/
            ├── SKILL.md         # Auto-invoked skill definition
            └── references/      # Supporting reference docs
```

## Adding a New Skill

1. Create a directory under the skill name
2. Add `.claude-plugin/plugin.json` with metadata
3. Add slash commands in `commands/` (user-invoked via `/name:command`)
4. Add auto-skills in `skills/` (model-invoked based on context)
5. Add an `AGENTS.md` to the source repo for agent-agnostic support
