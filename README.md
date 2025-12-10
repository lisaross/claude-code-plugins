# Lisa Ross's Claude Code Plugins

A marketplace of Claude Code plugins for workflow automation and productivity across any project type - software development, instructional design, product management, and more.

## What are Claude Code Plugins?

Claude Code plugins are extensions that enhance Claude Code with custom slash commands, specialized agents, hooks, and skills. Plugins can be shared across projects and teams, providing consistent tooling and workflows.

Learn more in the [official plugins documentation](https://code.claude.com/docs/en/plugins).

## Plugins in This Marketplace

| Name | Description | Contents |
| --- | --- | --- |
| [rules-migrate](./rules-migrate) | Migrate monolithic CLAUDE.md files to modular `.claude/rules/` directory. Works for any project type - software, instructional design, PM, product. | **Command:** `/rules-migrate:run` - Slash command entry point<br>**Agent:** `migrate` - Orchestrates migration workflow<br>**Skill:** `rules-migration` - Detailed migration instructions |

## Installation

### Option 1: Install from this marketplace (always latest)

1. Add this marketplace to Claude Code:

```bash
/plugin marketplace add lisaross/claude-code-plugins
```

2. Install a plugin:

```bash
/plugin install rules-migrate@lisaross
```

### Option 2: Fork for a stable version

If you want a point-in-time snapshot or to customize:

1. Fork this repo on GitHub
2. Add your fork as a marketplace:

```bash
/plugin marketplace add YOUR-USERNAME/claude-code-plugins
```

3. Install from your fork:

```bash
/plugin install rules-migrate@YOUR-USERNAME
```

### Browse available plugins

```bash
/plugin
```

## Contributing

When adding new plugins to this marketplace:

1. Create a new directory with your plugin name
2. Follow the standard plugin structure (see below)
3. Include a comprehensive README.md in your plugin directory
4. Add plugin metadata in `.claude-plugin/plugin.json`
5. Update the marketplace table in this README

## Plugin Structure

Each plugin follows the standard Claude Code plugin structure:

```text
plugin-name/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata
├── commands/                 # Slash commands (optional)
├── agents/                   # Specialized agents (optional)
├── skills/                   # Agent skills (optional)
├── hooks/                    # Event handlers (optional)
└── README.md                 # Plugin documentation
```

## Learn More

- [Claude Code Documentation](https://code.claude.com/docs/en/overview)
- [Plugin System Documentation](https://code.claude.com/docs/en/plugins)

## License

MIT

## Author

Lisa Ross (<lisa@makably.com>)
