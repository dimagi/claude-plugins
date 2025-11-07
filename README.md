# Claude Plugin Marketplace

A collection of workflow orchestration plugins and development utilities for Claude Code.

## Overview

This repository serves as a marketplace for Claude Code plugins, providing specialized agents, commands, and skills to enhance your development workflow.

## Plugins

### research-plan-build
Comprehensive workflow tools for codebase research, planning, and implementation with specialized agents for Django/Python projects.

This is based on the workflows described in https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/.

**Commands**
* `/research_codebase`: Step 1: before starting work on a task, look at the codebase and find code, patterns, files etc relevant to the task. Document the findings in `docs/claude/research`.
* `/create_plan`: Step 2: based on the task and the findings from step 1, create a detailed plan for the task. Write the plan to `docs/claude/plans`.
* `/iterate_plan`: Step 3: iterate on the plan from step 2 until it is ready to go.
* `/implement_plan`: Step 4: take a plan from step 2 / 3 and implement it.
* `/validate_plan`: Step 5: validate that the implementation from step 4 is correct.

**Agents**
* `codebase-analyzer`: A specialist at understanding HOW code works.
* `codebase-locator`: A specialist at finding WHERE code lives in a codebase.
* `codebase-pattern-finder`: A specialist at finding code patterns and examples in the codebase.
* `web-search-researcher`: An expert web research specialist focused on finding accurate, relevant information from web sources.

### dev-utils
Utility commands and skills for general development tasks.

**Commands**
* `/commit`: Create Git commits
* `/describe_pr`: Analyze a PR and write a detailed description following projects template.
  * This uses the GitHub CLI to get the PR details. If you want the command to update the PR with the new description, the GitHub CLI needs the `project` scope.
  * Use `gh auth refresh --scopes project`

## Installation

**Add Marketplace**
```
/plugin marketplace add dimagi/claude-plugins
```

**Browse Available Plugins**
```
/plugins
```
## License

See [LICENSE](LICENSE) for details.
