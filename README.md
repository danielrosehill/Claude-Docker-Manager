# Claude Docker Manager

A Claude Code workspace template for managing Docker environments. This repository provides a structured workspace that enables Claude Code to effectively administer Docker containers, compose stacks, and multi-environment deployments.

## Concept

This template implements the **Claude Code Workspace** pattern - a repository specifically structured to serve as a specialized environment for Claude Code. By combining:

- A comprehensive `CLAUDE.md` configuration
- Pre-built slash commands for common operations
- Specialized subagents for complex tasks
- Organized context storage for environment state

...you get an AI assistant that's immediately productive for Docker management without needing to explain your setup each session.

## Features

### Slash Commands

Quick-access commands for common Docker operations:

| Command | Description |
|---------|-------------|
| `/setup` | Initial environment discovery and configuration |
| `/status` | Health check of all containers and resources |
| `/cleanup` | Safely remove unused Docker resources |
| `/logs` | View and analyze container logs |
| `/deploy` | Deploy or manage Docker Compose stacks |
| `/backup` | Backup volumes and container data |
| `/update-context` | Refresh cached environment information |

### Subagents

Specialized agents for complex, multi-step tasks:

| Agent | Use Case |
|-------|----------|
| `container-diagnostics` | Debug crashes, restarts, connectivity issues |
| `compose-generator` | Generate production-ready compose files |
| `security-audit` | Audit for security misconfigurations |
| `migration-planner` | Plan migrations between environments |
| `resource-optimizer` | Analyze and optimize resource usage |

### Context Management

The `context/` directory stores persistent information about your Docker environments:

- **environments/**: Host specs, container inventories, configuration details
- **networks/**: Network topology documentation
- **volumes/**: Volume inventory and backup logs
- **images/**: Image catalog with metadata

This context enables Claude to make informed decisions without re-probing your environment each session.

## Getting Started

### 1. Clone the Template

```bash
git clone https://github.com/YOUR_USERNAME/Claude-Docker-Manager.git
cd Claude-Docker-Manager
```

### 2. Run Initial Setup

Open Claude Code in this directory and run:

```
/setup
```

This will:
- Probe your system hardware and Docker installation
- Inventory existing containers, images, networks, and volumes
- Ask configuration questions about how you'll use the workspace
- Generate initial context files

### 3. Start Managing Docker

Use slash commands for quick operations:
- `/status` to check environment health
- `/deploy` to create new stacks
- `/backup` before making major changes

## Directory Structure

```
.
├── CLAUDE.md              # Claude Code configuration
├── README.md              # This file
├── .gitignore             # Excludes sensitive files
├── .claude/
│   ├── commands/          # Slash command definitions
│   │   ├── setup.md
│   │   ├── status.md
│   │   ├── cleanup.md
│   │   ├── logs.md
│   │   ├── deploy.md
│   │   ├── backup.md
│   │   └── update-context.md
│   └── agents/            # Subagent definitions
│       ├── container-diagnostics.md
│       ├── compose-generator.md
│       ├── security-audit.md
│       ├── migration-planner.md
│       └── resource-optimizer.md
├── context/
│   ├── environments/      # Per-environment profiles
│   ├── networks/          # Network documentation
│   ├── volumes/           # Volume inventory
│   └── images/            # Image catalog
├── stacks/                # Docker Compose stacks
└── scripts/               # Utility scripts
```

## Multi-Environment Management

This workspace can manage multiple Docker environments:

- **Local**: The Docker installation on your current machine
- **Remote**: Docker hosts accessible via SSH

For remote environments, Claude uses SSH (via bash aliases or Tailscale names) to execute Docker commands. Each environment gets its own profile in `context/environments/`.

## Stack Management

When deploying Docker Compose stacks, you have options:

1. **In-repo**: Store in `stacks/` directory - simple version control
2. **Submodule**: Link separate repos - independent versioning per stack
3. **External**: Store elsewhere - no coupling to this repo

Claude will ask your preference before creating stacks.

## Customization

### Adding Commands

Create new `.md` files in `.claude/commands/` to add custom slash commands. The filename becomes the command name.

### Adding Agents

Create new `.md` files in `.claude/agents/` with YAML frontmatter:

```yaml
---
name: my-agent
description: What this agent does
tools:
  - Bash
  - Read
  - Write
---

# Agent instructions here...
```

### Extending Context

Add new subdirectories to `context/` for additional persistent information (e.g., `context/backups/`, `context/deployments/`).

## Security Considerations

- Never commit `.env` files with real secrets
- The `.gitignore` excludes common sensitive patterns
- Use environment variables or secrets management for credentials
- Review the `security-audit` agent output periodically

## License

MIT License - Feel free to use and adapt this template for your own Docker management needs.

## Contributing

Contributions welcome! If you've added useful commands or agents, please submit a PR.
