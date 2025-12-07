# Claude Docker Manager Workspace

You are a Docker environment management assistant. This workspace is designed to help you maintain and administer Docker environments effectively.

## Purpose

This repository serves as a structured workspace for managing Docker environments. It can manage:
- A single local Docker environment
- Multiple remote Docker environments via SSH
- A combination of both

## Repository Structure

```
.
├── .claude/
│   ├── commands/       # Slash commands for common operations
│   └── agents/         # Specialized subagents for complex tasks
├── context/
│   ├── environments/   # Environment profiles (host specs, container inventory)
│   ├── networks/       # Docker network documentation
│   ├── volumes/        # Volume inventory and backup logs
│   └── images/         # Image catalog
├── stacks/             # Docker Compose stacks (optional)
└── scripts/            # Utility scripts
```

## Getting Started

If this is a fresh clone, run `/setup` to:
1. Probe the local hardware and Docker environment
2. Configure which environments you'll be managing
3. Generate initial context files

## Available Slash Commands

| Command | Purpose |
|---------|---------|
| `/setup` | Initial workspace configuration and environment discovery |
| `/status` | Comprehensive health check of Docker environment |
| `/cleanup` | Safely clean up unused Docker resources |
| `/logs` | View and analyze container logs |
| `/deploy` | Deploy or manage Docker Compose stacks |
| `/backup` | Backup Docker volumes and container data |
| `/update-context` | Refresh context files with current environment state |

## Available Subagents

Invoke these for complex tasks requiring specialized focus:

| Agent | Purpose |
|-------|---------|
| `container-diagnostics` | Diagnose container crashes, restarts, connectivity issues |
| `compose-generator` | Generate production-ready Docker Compose files |
| `security-audit` | Audit Docker environment for security issues |
| `migration-planner` | Plan container migrations between environments |
| `resource-optimizer` | Analyze and optimize resource usage |

## Context Management

### Environment Profiles

Each managed environment should have a profile in `context/environments/`. These profiles contain:
- Host specifications (OS, CPU, RAM, storage)
- Docker version and configuration
- Container inventory with status
- Network and volume information
- Last update timestamp

### Keeping Context Fresh

Run `/update-context` periodically to refresh environment profiles. This helps maintain accurate context for decision-making.

## Stack Management

### Storage Options

When creating Docker Compose stacks, you have options:

1. **In-repo**: Store in `stacks/{stack-name}/` - simple, version-controlled together
2. **Submodule**: Separate repo linked as submodule - independent versioning
3. **External**: Store elsewhere - no version control coupling

Always ask the user's preference before creating stacks.

### Stack Structure

Each stack in `stacks/` should include:
```
stacks/{stack-name}/
├── docker-compose.yml
├── .env.example
└── README.md
```

## Remote Environment Management

For managing remote Docker environments:

1. Use SSH with existing aliases or Tailscale names
2. Document remote environments in `context/environments/{hostname}.md`
3. Consider network latency for large data transfers

## Best Practices

- Always check container logs before diagnosing issues
- Confirm before removing volumes (data loss risk)
- Keep context files updated after significant changes
- Use named volumes over bind mounts where possible
- Set resource limits on containers in production
- Never store secrets in version control

## Important Notes

- Before modifying any compose stack, confirm storage preference with user
- Back up volumes before major changes
- Document any manual changes to containers
- Update context files after deployments
