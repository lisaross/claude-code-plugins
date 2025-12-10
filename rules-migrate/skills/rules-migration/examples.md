# Examples: CLAUDE.md to Rules Migration

This file provides complete before/after examples of converting CLAUDE.md files to the `.claude/rules/` system for various project types.

## Example 1: Instructional Design Project

### Before: CLAUDE.md (250 lines)

```markdown
# Claude Code Configuration

## Project Context
This is a corporate training development project.
Client: Acme Corporation
Timeline: Q1 2025

## Content Standards

### Writing Style
- Use active voice
- Keep sentences under 20 words
- Write at 8th grade reading level
- Avoid jargon unless defined

### Learning Objectives
- Start with action verbs (Bloom's taxonomy)
- Make measurable and specific
- Align with assessment criteria

## Course Development

### Module Structure
- Introduction with learning objectives
- Core content (10-15 minutes per section)
- Knowledge check every 5 minutes
- Summary and key takeaways
- Assessment

### Multimedia Guidelines
- Videos under 6 minutes
- Include closed captions
- Provide transcripts
- Alt text for all images

## Assessment Design

### Quiz Questions
- 4-5 answer choices
- One clearly correct answer
- Plausible distractors
- Avoid "all of the above"

### Scenario-Based
- Real-world situations
- Decision points
- Consequences feedback

## Accessibility

- WCAG 2.1 AA compliance
- Screen reader compatible
- Keyboard navigation
- Color contrast 4.5:1 minimum

## Deliverables

### File Naming
- Course_Module_Section_Version.ext
- Example: ACM_M01_S02_v1.docx

### Review Process
- SME review → Revisions → QA → Final
```

### After: .claude/rules/ Structure

```text
.claude/rules/
├── core.md
├── content-standards.md
├── course-development.md
├── assessment.md
├── accessibility.md
└── deliverables.md
```

**core.md** (no frontmatter - applies globally):

```markdown
# Project Standards

## Context
Corporate training development for Acme Corporation.
Timeline: Q1 2025

## Quality Gates
Before marking ANY deliverable complete:
1. Verify learning objectives alignment
2. Check accessibility compliance
3. Run through review checklist
```

**content-standards.md**:

```markdown
# Content Writing Standards

## Writing Style
- Use active voice
- Keep sentences under 20 words
- Write at 8th grade reading level
- Avoid jargon unless defined in glossary

## Learning Objectives
- Start with action verbs (Bloom's taxonomy)
- Make measurable and specific
- Align with assessment criteria
- Format: "After completing this module, learners will be able to..."
```

**assessment.md**:

```markdown
# Assessment Design

## Quiz Questions
- 4-5 answer choices per question
- One clearly correct answer
- Plausible distractors based on common misconceptions
- Avoid "all of the above" or "none of the above"

## Scenario-Based Assessments
- Ground in real-world situations
- Include meaningful decision points
- Provide consequence-based feedback
- Connect to job performance
```

---

## Example 2: Product Management Project

### Before: CLAUDE.md (300 lines)

```markdown
# Claude Code Configuration

## Product Context
B2B SaaS product for HR teams
Target: Mid-market companies (100-1000 employees)
Stage: Growth phase

## Documentation Standards

### PRDs
- Problem statement first
- User stories with acceptance criteria
- Success metrics defined
- Technical constraints noted

### User Stories
Format: As a [persona], I want [goal], so that [benefit]

Acceptance Criteria:
- Given/When/Then format
- Edge cases covered
- Non-functional requirements

## Research

### User Interviews
- 5-7 participants minimum
- Mix of power users and new users
- Record with permission
- Synthesize within 48 hours

### Competitive Analysis
- Feature comparison matrix
- Pricing analysis
- Positioning map
- Update quarterly

## Prioritization

### Framework
Use RICE scoring:
- Reach: How many users affected
- Impact: How much improvement
- Confidence: How sure are we
- Effort: Engineering weeks

### Roadmap
- Now: Current sprint
- Next: Next 2 sprints
- Later: 3+ sprints out
- Icebox: Someday/maybe

## Stakeholder Communication

### Weekly Updates
- Progress on OKRs
- Blockers and risks
- Decisions needed
- Wins to celebrate

### Launch Communication
- Internal: 2 weeks before
- External: 1 week before
- Support team: Training complete before launch
```

### After: .claude/rules/ Structure

```text
.claude/rules/
├── core.md
├── documentation/
│   ├── prds.md
│   └── user-stories.md
├── research/
│   ├── user-interviews.md
│   └── competitive.md
├── prioritization.md
└── communication.md
```

**core.md**:

```markdown
# Product Standards

## Context
B2B SaaS for HR teams
Target: Mid-market (100-1000 employees)
Stage: Growth

## Principles
- User problems first, solutions second
- Data-informed decisions
- Ship small, learn fast
- Cross-functional collaboration
```

**documentation/prds.md**:

```markdown
# PRD Standards

## Structure
1. Problem Statement (what pain are we solving?)
2. User Stories with Acceptance Criteria
3. Success Metrics (how will we measure?)
4. Technical Constraints
5. Dependencies and Risks
6. Timeline

## Quality Checklist
- [ ] Problem validated with user research
- [ ] Success metrics are measurable
- [ ] Engineering has reviewed feasibility
- [ ] Design has provided mocks
- [ ] Stakeholders have signed off
```

---

## Example 3: Project Management Office

### Before: CLAUDE.md (280 lines)

```markdown
# Claude Code Configuration

## PMO Standards

### Project Initiation
- Business case required for projects > $50k
- Sponsor identified and committed
- Success criteria defined
- Resource requirements estimated

### Planning
- Work breakdown structure
- Critical path identified
- Risk register created
- Communication plan established

## Status Reporting

### Weekly Status
- Red/Amber/Green overall status
- Accomplishments this week
- Plans for next week
- Risks and issues
- Decisions needed

### Monthly Executive Summary
- Portfolio health dashboard
- Budget vs actual
- Resource utilization
- Key milestones achieved/missed

## Risk Management

### Risk Categories
- Technical
- Resource
- Schedule
- Budget
- External/Dependencies

### Response Strategies
- Avoid: Change plan to eliminate
- Mitigate: Reduce probability/impact
- Transfer: Shift to third party
- Accept: Acknowledge and monitor

## Meeting Standards

### Stand-ups
- 15 minutes max
- What did you do? What will you do? Blockers?
- Parking lot for detailed discussions

### Retrospectives
- What went well?
- What could improve?
- Action items with owners
```

### After: .claude/rules/ Structure

```text
.claude/rules/
├── core.md
├── initiation.md
├── planning.md
├── reporting/
│   ├── weekly.md
│   └── monthly.md
├── risk-management.md
└── meetings.md
```

**reporting/weekly.md**:

```markdown
# Weekly Status Report Standards

## Required Sections

### Overall Status (RAG)
- **Green**: On track, no issues
- **Amber**: Minor issues, mitigation in progress
- **Red**: Significant issues, escalation needed

### Content
1. **Accomplishments**: What was completed this week
2. **Plans**: What's planned for next week
3. **Risks & Issues**: New or escalated items
4. **Decisions Needed**: Items requiring sponsor input

## Submission
- Due: Friday 4pm
- Format: PowerPoint template
- Distribution: Sponsor + steering committee
```

---

## Example 4: Software Development (Full-Stack)

### Before: CLAUDE.md (400 lines)

```markdown
# Claude Code Configuration

## Tech Stack
- Frontend: Next.js 14, React, Tailwind
- Backend: Convex
- Auth: Clerk
- Deployment: Cloudflare Pages

## Code Standards

### TypeScript
- Strict mode enabled
- No `any` types
- Interfaces for props
- Zod for runtime validation

### React
- Functional components only
- Custom hooks for reusable logic
- Server components where possible

### API Design
- RESTful conventions
- Consistent error responses
- Input validation on all endpoints

## Testing

### Unit Tests
- Vitest for unit tests
- 80% coverage target
- Test business logic first

### E2E Tests
- Playwright for E2E
- Critical user flows
- Run before deploy

## Git Workflow

### Commits
Format: type(scope): description
Types: feat, fix, docs, refactor, test, chore

### Pull Requests
- Link to issue
- Description of changes
- Screenshots for UI changes
- Tests passing
```

### After: .claude/rules/ Structure

```text
.claude/rules/
├── core.md
├── stack.md
├── frontend/
│   ├── react.md          # paths: src/**/*.tsx
│   └── styles.md         # paths: **/*.css
├── backend/
│   └── api.md            # paths: convex/**/*.ts
├── testing.md
└── git.md
```

**frontend/react.md** (with path frontmatter):

```yaml
---
paths: src/**/*.tsx
---
```

```markdown
# React Standards

## Components
- Functional components only (no classes)
- Custom hooks for reusable logic
- Server components where possible

## Props
- Define interfaces for all props
- Use TypeScript generics for reusable components
- Destructure props in function signature

## Example

interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
}

export function Button({ label, onClick, variant = 'primary' }: ButtonProps) {
  return (
    <button onClick={onClick} className={styles[variant]}>
      {label}
    </button>
  );
}
```

**backend/api.md** (with path frontmatter):

```yaml
---
paths: convex/**/*.ts
---
```

```markdown
# Convex Backend Standards

## Queries
- Use indexed fields for filtering
- Return minimal data needed
- Handle empty states gracefully

## Mutations
- Validate inputs with Convex validators
- Return the created/updated record
- Use transactions for multi-step operations

## Error Handling
- Throw ConvexError for user-facing errors
- Log unexpected errors for debugging
- Never expose internal details to clients
```

---

## Key Takeaways

### When to Use Path-Specific Rules

**Use paths frontmatter when:**
- Rules only apply to certain file types
- Different standards for different areas (frontend vs backend)
- Team members work in specific areas

**Don't use paths frontmatter when:**
- Rules apply project-wide (communication standards, meeting formats)
- Rules are about process, not files
- Content is non-technical (PM, instructional design)

### Organization Patterns

| Project Type | Recommended Structure |
|--------------|----------------------|
| Software Dev | By layer: `frontend/`, `backend/`, `testing/` |
| Instructional Design | By phase: `design/`, `development/`, `review/` |
| Product Management | By activity: `research/`, `documentation/`, `communication/` |
| Project Management | By process: `planning/`, `execution/`, `reporting/` |

### File Naming

- Use kebab-case: `user-stories.md`, `risk-management.md`
- Be descriptive: `weekly-status.md` not `weekly.md`
- Group related files in subdirectories

---

*Examples updated: 2025-12-10*
