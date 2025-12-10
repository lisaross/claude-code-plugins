# Reference: Rules System Deep Dive

This document provides detailed technical reference for Claude Code's `.claude/rules/` system, based on the [official documentation](https://code.claude.com/docs/en/memory#modular-rules-with-claude/rules/).

## Table of Contents

- [Rules System Overview](#rules-system-overview)
- [Glob Pattern Syntax](#glob-pattern-syntax)
- [YAML Frontmatter](#yaml-frontmatter)
- [Directory Organization Patterns](#directory-organization-patterns)
- [Migration Strategies](#migration-strategies)
- [Best Practices](#best-practices)

---

## Rules System Overview

### How Rules Work

Claude Code automatically loads all `.md` files from `.claude/rules/` as project memory:

1. **At startup**: When Claude Code initializes in a project
2. **Recursively**: Loads files from subdirectories
3. **Path-aware**: Applies conditional rules based on file context
4. **Priority**: Project rules have higher priority than user-level rules

### Memory Hierarchy

| Memory Type | Location | Purpose |
|-------------|----------|---------|
| **Project memory** | `./CLAUDE.md` or `./.claude/CLAUDE.md` | Team-shared instructions |
| **Project rules** | `./.claude/rules/*.md` | Modular, topic-specific instructions |
| **User memory** | `~/.claude/CLAUDE.md` | Personal preferences (all projects) |
| **User rules** | `~/.claude/rules/*.md` | Personal rules (all projects) |
| **Local memory** | `./CLAUDE.local.md` | Personal project-specific (gitignored) |

Rules in `.claude/rules/` have the same priority as `.claude/CLAUDE.md`.

### Rules vs CLAUDE.md

Both serve the same purpose (instructions for Claude), but:

- **CLAUDE.md**: Single file, good for smaller projects
- **`.claude/rules/`**: Multiple files, better for larger projects with distinct concerns

You can use both together - they complement each other.

---

## Glob Pattern Syntax

### Basic Patterns

| Pattern | Matches | Example |
|---------|---------|---------|
| `*.ts` | `.ts` files in project root only | `app.ts`, `utils.ts` |
| `**/*.ts` | All `.ts` files in any directory | `src/app.ts`, `src/api/users.ts` |
| `src/**/*` | All files under `src/` | Any file type in src tree |
| `src/**/*.tsx` | All `.tsx` files under `src/` | `src/components/Button.tsx` |
| `src/components/*.tsx` | `.tsx` files in specific directory | `src/components/Button.tsx` |

### Brace Expansion

Use braces to match multiple patterns efficiently:

```yaml
---
paths: src/**/*.{ts,tsx}
---
```

This expands to match both `src/**/*.ts` and `src/**/*.tsx`.

### Multiple Patterns

Combine multiple patterns with commas:

```yaml
---
paths: {src,lib}/**/*.ts, tests/**/*.test.ts
---
```

---

## YAML Frontmatter

### Basic Syntax

Path-specific rules use YAML frontmatter with the `paths` field:

```yaml
---
paths: src/api/**/*.ts
---

# API Development Rules

- All API endpoints must include input validation
- Use the standard error response format
```

### No Frontmatter = Global Rules

Rules without a `paths` field are loaded unconditionally and apply to all files:

```markdown
# Core Execution Rules

ALWAYS commit after meaningful changes.
```

### Frontmatter Examples

**Single pattern:**

```yaml
---
paths: src/api/**/*.ts
---
```

**Multiple patterns with braces:**

```yaml
---
paths: src/**/*.{ts,tsx}
---
```

**Multiple patterns with commas:**

```yaml
---
paths: {src,lib}/**/*.ts, tests/**/*.test.ts
---
```

### Field Name

The field must be `paths` (plural). Using `path` (singular) will not work.

---

## Directory Organization Patterns

### Pattern 1: Flat Structure (Simple Projects)

**Use for**: Small projects, fewer than 5 rule files

```text
.claude/rules/
├── code-style.md     # Code style guidelines
├── testing.md        # Testing conventions
└── security.md       # Security requirements
```

**Pros**: Simple, easy to navigate
**Cons**: Doesn't scale well

### Pattern 2: Layered Structure (Medium Projects)

**Use for**: Projects with clear frontend/backend split

```text
.claude/rules/
├── code-style.md
├── testing.md
├── frontend/
│   ├── react.md
│   └── styles.md
└── backend/
    ├── api.md
    └── database.md
```

**Pros**: Clear separation of concerns
**Cons**: Requires more navigation

### Pattern 3: Deep Structure (Large Projects)

**Use for**: Large projects, monorepos

```text
.claude/rules/
├── core/
│   ├── code-quality.md
│   └── git-workflow.md
├── frontend/
│   ├── react/
│   │   ├── components.md
│   │   └── hooks.md
│   └── styles/
│       └── tailwind.md
└── backend/
    ├── api/
    │   └── rest.md
    └── database/
        └── schema.md
```

All `.md` files are discovered recursively.

### User-Level Rules

Personal rules that apply to all your projects go in `~/.claude/rules/`:

```text
~/.claude/rules/
├── preferences.md    # Your personal coding preferences
└── workflows.md      # Your preferred workflows
```

User-level rules are loaded before project rules, giving project rules higher priority.

---

## Migration Strategies

### Strategy 1: Single-Pass (Small CLAUDE.md)

**For**: Files under 300 lines

1. Read entire CLAUDE.md
2. Identify 3-7 major sections
3. Create rule file for each section
4. Add `paths` frontmatter where applicable
5. Archive original CLAUDE.md

**Time**: 15-30 minutes

### Strategy 2: Iterative (Medium CLAUDE.md)

**For**: Files 300-800 lines

1. **Phase 1**: Extract core/critical rules
2. **Phase 2**: Extract frontend rules
3. **Phase 3**: Extract backend rules
4. **Phase 4**: Extract workflow rules (git, testing)
5. Verify each phase before proceeding

**Time**: 45-90 minutes

### Strategy 3: Gradual (Large or Critical Projects)

**For**: Files 800+ lines or mission-critical projects

1. Create `.claude/rules/` alongside existing CLAUDE.md
2. Migrate one section at a time over days/weeks
3. Run both systems in parallel for validation
4. Archive CLAUDE.md only after full validation

**Time**: 1-2 weeks (safe, low-risk)

---

## Best Practices

From the official documentation:

### Rule File Design

- **Keep rules focused**: Each file should cover one topic (e.g., `testing.md`, `api-design.md`)
- **Use descriptive filenames**: The filename should indicate what the rules cover
- **Use conditional rules sparingly**: Only add `paths` frontmatter when rules truly apply to specific file types
- **Organize with subdirectories**: Group related rules (e.g., `frontend/`, `backend/`)

### Content Guidelines

- **Be specific**: "Use 2-space indentation" is better than "Format code properly"
- **Use structure**: Format each memory as a bullet point, group under descriptive headings
- **Review periodically**: Update as your project evolves

### Symlinks

The `.claude/rules/` directory supports symlinks for sharing common rules across projects:

```bash
# Symlink a shared rules directory
ln -s ~/shared-claude-rules .claude/rules/shared

# Symlink individual rule files
ln -s ~/company-standards/security.md .claude/rules/security.md
```

---

## Quick Reference

### Supported Patterns

| Pattern | Description |
|---------|-------------|
| `**/*.ts` | All TypeScript files |
| `src/**/*` | All files under src/ |
| `*.md` | Markdown files in root |
| `src/components/*.tsx` | TSX in specific directory |
| `**/*.{ts,tsx}` | Multiple extensions |
| `{src,lib}/**/*.ts` | Multiple directories |

### File Locations

| Location | Auto-loaded | Shared |
|----------|-------------|--------|
| `.claude/rules/*.md` | Yes | Yes (via git) |
| `~/.claude/rules/*.md` | Yes | No (personal) |
| `.claude/CLAUDE.md` | Yes | Yes (via git) |
| `CLAUDE.local.md` | Yes | No (gitignored) |

---

## Additional Resources

- [Claude Code Memory Documentation](https://code.claude.com/docs/en/memory)
- [Modular Rules Section](https://code.claude.com/docs/en/memory#modular-rules-with-claude/rules/)

---

*Based on official Claude Code documentation | Updated: 2025-12-10*
