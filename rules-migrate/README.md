# rules-migrate

Migrate monolithic `CLAUDE.md` files to the modular `.claude/rules/` directory system.

## Overview

Claude Code's [modular rules system](https://code.claude.com/docs/en/memory#modular-rules-with-claude/rules/) allows you to organize project instructions into focused rule files. This plugin automates the conversion process for **any project type** - software development, instructional design, product management, project management, and more.

### Before: Monolithic CLAUDE.md

```text
.claude/CLAUDE.md (500+ lines)
├── Project context
├── Quality standards
├── Process guidelines
├── Communication rules
├── Deliverable formats
└── Review checklists
```

### After: Modular Rules

```text
.claude/rules/
├── core.md                 # Global standards
├── quality.md              # Quality gates
├── communication/
│   ├── weekly-status.md
│   └── stakeholders.md
└── deliverables/
    ├── formats.md
    └── review-process.md
```

## Installation

### From the marketplace (always latest)

```bash
/plugin marketplace add lisaross/claude-code-plugins
/plugin install rules-migrate@lisaross
```

### Fork for a stable version

For a point-in-time snapshot, fork the repo and install from your fork:

```bash
/plugin marketplace add YOUR-USERNAME/claude-code-plugins
/plugin install rules-migrate@YOUR-USERNAME
```

## Usage

### Slash Command

```bash
# Auto-detect and migrate CLAUDE.md
/rules-migrate:run

# Migrate specific file
/rules-migrate:run ./.claude/CLAUDE.md
```

### Trigger Phrases

Say any of these to invoke the skill:

- "migrate claudemd to rules"
- "convert claude.md to rules"
- "modularize claude.md"
- "migrate to rules system"

## Contents

| Type | Name | Description |
| --- | --- | --- |
| Agent | `migrate` | Orchestrates the migration workflow |
| Command | `/run` | Slash command entry point |
| Skill | `rules-migration` | Detailed migration instructions |

## How It Works

1. **Read & Analyze**: Parses CLAUDE.md to identify sections
2. **Plan Structure**: Maps sections to rule files
3. **Create Rules**: Extracts content into `.claude/rules/`
4. **Add Frontmatter**: Adds `paths` for conditional rules
5. **Validate**: Ensures no content lost
6. **Archive**: Backs up original CLAUDE.md

## Path-Specific Rules (Optional)

For software projects, rules can target specific files using YAML frontmatter:

```yaml
---
paths: src/api/**/*.ts
---

# API Development Rules

- All endpoints must have error handling
- Use Zod for request validation
```

For non-code projects (instructional design, PM, product), most rules apply globally and don't need `paths` frontmatter.

### Supported Glob Patterns

| Pattern | Matches |
|---------|---------|
| `**/*.ts` | All TypeScript files |
| `src/**/*` | All files under src/ |
| `**/*.{ts,tsx}` | Multiple extensions |
| `{src,lib}/**/*.ts` | Multiple directories |

## Documentation

- [SKILL.md](skills/rules-migration/SKILL.md) - Full workflow guide
- [reference.md](skills/rules-migration/reference.md) - Technical reference
- [examples.md](skills/rules-migration/examples.md) - Before/after examples

## Testing the Plugin

To verify the plugin works correctly after installation:

### 1. Verify Installation

```bash
# Check the plugin is installed
/plugin

# Should show rules-migrate@lisaross as installed
```

### 2. Test the Slash Command

```bash
# In a project with a CLAUDE.md file
/rules-migrate:run
```

**Expected behavior:**
- Claude reads your CLAUDE.md file
- Proposes a directory structure for `.claude/rules/`
- Creates rule files with appropriate content
- Archives original CLAUDE.md

### 3. Test Skill Trigger

Say one of the trigger phrases in a project with CLAUDE.md:

> "migrate claudemd to rules"

**Expected behavior:** Same as slash command - Claude should begin the migration workflow.

### 4. Verify Results

After migration, check:

```bash
# Rules directory created
ls -la .claude/rules/

# Original backed up
ls -la .claude/CLAUDE.md.backup

# Rules are loaded (restart Claude Code first)
/memory
```

### 5. Test with Sample Content

Create a test CLAUDE.md with multiple sections:

```markdown
# Project Config

## Code Quality
- Run tests before commit

## Frontend
- Use React hooks

## Backend
- Validate all inputs
```

Run the migration and verify each section becomes a separate rule file.

## Learn More

- [Claude Code Memory Documentation](https://code.claude.com/docs/en/memory)
- [Modular Rules Documentation](https://code.claude.com/docs/en/memory#modular-rules-with-claude/rules/)
