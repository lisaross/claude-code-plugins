---
description: Migrate CLAUDE.md to modular .claude/rules/ directory structure
args: [source-path]
---

Migrate a CLAUDE.md file to Claude Code's modular `.claude/rules/` system.

## User Input

{{args}}

## CRITICAL: Execution Requirements

**You MUST follow these steps in order. Announce each step before executing.**

1. **FIRST**: Output "🔄 Starting CLAUDE.md migration..."
2. **SECOND**: Use the Task tool to invoke the migrate agent (see below)
3. **THIRD**: Report results when agent completes

**DO NOT** just describe what you would do. **ACTUALLY EXECUTE** the Task tool.

## Instructions

### Parse Arguments

Extract from `{{args}}`:
- `source-path`: Path to CLAUDE.md file (optional, defaults to auto-detection)

### Locate CLAUDE.md

If no path provided, search in order:
1. `./.claude/CLAUDE.md`
2. `./CLAUDE.md`
3. Ask user to specify path

### Execute Migration

Use the Task tool to invoke the migrate agent:

```
Task(
  subagent_type: "migrate",
  prompt: "Migrate CLAUDE.md at {{source-path}} to .claude/rules/ directory structure"
)
```

The agent will:
1. Invoke the `rules-migration` skill
2. Follow the skill's workflow to migrate content
3. Create organized rule files with path-specific frontmatter
4. Archive the original CLAUDE.md
5. Commit the changes

### Output

After completion, display:

```markdown
## Migration Complete

**Source**: {source-path}
**Destination**: .claude/rules/

### Created Files

- .claude/rules/core.md
- .claude/rules/...
- (list all created files)

### Archived

- .claude/CLAUDE.md.backup

### Next Steps

1. Review the new rule files
2. Adjust organization if needed
3. Run `/memory` to verify rules are loaded
```

## Examples

**Migrate default CLAUDE.md:**

```bash
/rules-migrate:run
```

**Migrate specific file:**

```bash
/rules-migrate:run ./.claude/CLAUDE.md
```

## Notes

- All original content is preserved during migration
- Original file is backed up, not deleted
- Rules without path patterns apply globally
- Rules with `paths` frontmatter apply conditionally
