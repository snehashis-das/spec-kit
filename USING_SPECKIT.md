# Spec-Kit Workflow Guide for gh-metrics

## Overview

This guide shows how to use **spec-kit AI workflows** for structured development on gh-metrics. Spec-kit provides generic workflows (analyze → specify → plan → implement) that work across any project.

**For direct Copilot usage without spec-kit**, see [Working with Copilot](WORKING_WITH_COPILOT.md).

## Spec-Kit Agents (User-Level)

| Agent                   | Purpose                  | When to Use                                              |
| ----------------------- | ------------------------ | -------------------------------------------------------- |
| `@speckit.analyze`      | Understand existing code | Before making changes to unfamiliar code                 |
| `@speckit.clarify`      | Get clear requirements   | When request is ambiguous                                |
| `@speckit.specify`      | Create detailed specs    | Designing new features or major changes                  |
| `@speckit.plan`         | Break down into tasks    | Multi-step implementation                                |
| `@speckit.implement`    | Execute implementation   | Following a plan                                         |
| `@speckit.tasks`        | Track progress           | Complex work with many steps                             |
| `@speckit.constitution` | Reference principles     | Verify compliance with `.specify/memory/constitution.md` |

## gh-metrics Tools (Project-Level)

| Tool                                  | Purpose                       |
| ------------------------------------- | ----------------------------- |
| `@quality-enforcer`                   | NFR compliance validation     |
| `.github/prompts/add-new-metric.md`   | Metric implementation pattern |
| `.github/prompts/customize-charts.md` | Chart styling guide           |
| `docs/TROUBLESHOOTING.md`             | User troubleshooting guide    |

## Quick Workflows

### Adding a New Metric (Spec-Kit Approach)

```bash
# 1. Clarify requirements
@speckit.clarify "Add code review approval time metric"

# 2. Analyze existing patterns
@speckit.analyze "Review libs/collectors/pr_collector.py and libs/reports/pr_analytics.py"

# 3. Create specification
@speckit.specify "Create spec for approval time metric following UC-1 pattern"

# 4. Quality check first
@quality-enforcer "Review pr_collector.py before adding approval metric"

# 5. Plan implementation
@speckit.plan "Plan approval time metric implementation"

# 6. Implement
@speckit.implement "Following the plan, implement approval time metric"

# 7. Validate
@quality-enforcer "Review approval time implementation against NFRs"
```

### Refactoring (Spec-Kit Approach)

```bash
# 1. Identify issues
@quality-enforcer "Analyze libs/reports/ for code duplication"

# 2. Plan refactoring
@speckit.plan "Plan extraction of duplicated chart generation pattern"

# 3. Check constitution
@speckit.constitution "Verify refactoring maintains separation of concerns"

# 4. Implement
@speckit.implement "Execute refactoring plan"

# 5. Validate
@quality-enforcer "Verify duplication reduced below 5%"
```

### Simple Changes (Direct Copilot - No Spec-Kit)

For straightforward tasks, skip spec-kit and work directly:

```bash
# Adding a repository
"Add owner/repo to conf/my_config.ini with workflow filters for main branch"

# Fixing a bug
"Fix the CSV float formatting issue in csv_utils.py"

# Customizing a chart
"Change PR analytics chart to show weekly trends instead of monthly"
```

**See [Working with Copilot](../docs/WORKING_WITH_COPILOT.md) for direct usage patterns.**

## When to Use Spec-Kit vs Direct

| Use Spec-Kit              | Use Direct Copilot      |
| ------------------------- | ----------------------- |
| New feature design        | Config file updates     |
| Complex refactoring       | Bug fixes               |
| Unfamiliar codebase       | Chart customization     |
| Multi-step implementation | Adding repositories     |
| Need specification        | Simple metric additions |

## Quality Gates

Both approaches use same quality enforcement:

- ✅ `@quality-enforcer` reviews against constitution NFRs
- ✅ Pre-commit hooks run automatically
- ✅ Architecture patterns from `.github/copilot-instructions.md`
- ✅ Constitution compliance (`.specify/memory/constitution.md`)

## Getting Started

1. **Read**: `.specify/memory/constitution.md` (project rules)
2. **Reference**: `.github/copilot-instructions.md` (architecture patterns)
3. **Choose**: Spec-kit (complex) or Direct (simple)
4. **Validate**: Use `@quality-enforcer` for compliance

## Resources

- **Constitution**: `.specify/memory/constitution.md` - NFRs and governance
- **Architecture**: `.github/copilot-instructions.md` - Patterns and conventions
- **Requirements**: `docs/functional-requirements.md` - Use case specs
- **Direct Usage**: `docs/WORKING_WITH_COPILOT.md` - Non-spec-kit workflows
- **Task Guides**: `.github/prompts/` - Repo-specific templates (add metric, refactor, etc.)
