# Claude Plugin Marketplace

A collection of workflow orchestration plugins and development utilities for Claude Code.

## Overview

This repository serves as a marketplace for Claude Code plugins, providing specialized agents, commands, and skills to enhance your development workflow.

## Plugins

### dev-utils
Utility commands for general development tasks.

**Commands**
* `/resolve-pr-comments`: Fetch all unresolved review threads on the current branch's PR, evaluate each one, apply fixes where warranted, reply, and optionally resolve threads.
  * `--resolve`: resolve each thread after replying
  * `--dry-run`: print the evaluation plan but make no changes

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
