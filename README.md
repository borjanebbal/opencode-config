# Opencode Configuration

Personal multi-agent configuration for [Opencode](https://opencode.ai) — a programmable AI development environment with scoped agents, permission controls, and external skill packs.

---

## Agent Architecture

The configuration follows a role-based multi-agent design:


### 🏗️ `design`
Staff-level architecture agent.

- Produces structured system designs
- Surfaces tradeoffs and risks
- Outputs phased implementation plans
- Cannot modify files or execute commands


### 🛠️ `build`
Implementation agent.

- Follows architectural plans strictly
- Writes production-ready code
- Generates minimal, focused tests
- Uses scoped frontend/backend skills


### ♻️ `refactor`
Behavior-preserving improvement agent.

- Improves readability and maintainability
- Applies SOLID principles
- Avoids unnecessary abstraction
- Preserves public APIs and behavior


### 🔍 `review`
Merge-gate reviewer.

- Detects correctness issues
- Flags performance and security risks
- Classifies severity (low / medium / high)
- Explicitly states merge safety

---

## External Skill Packs

| Pack | Source | Skills |
|------|--------|--------|
| Engineering Team | [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) | `senior-architect`, `senior-devops`, `senior-security`, `senior-qa`, `senior-fullstack`, `senior-frontend`, `senior-backend`, `code-reviewer` |
| Vercel Agent | [vercel-labs/agent-skills](https://skills.sh/vercel-labs/agent-skills) | `web-design-guidelines`, `vercel-react-best-practices` |
| Vue | [hyf0/vue-skills](https://skills.sh/hyf0/vue-skills/vue-best-practices) | `vue-best-practices` |
| NestJS | [kadajett/agent-nestjs-skills](https://skills.sh/kadajett/agent-nestjs-skills/nestjs-best-practices) | `nestjs-best-practices` |
| MCP Builder | [anthropics/skills](https://skills.sh/anthropics/skills/mcp-builder) | `mcp-builder` |

---

## Model Configuration

This setup uses GitHub Copilot-hosted models:

- `github-copilot/claude-sonnet-4.6`
- `github-copilot/claude-opus-4.6`
- `github-copilot/gpt-5.3-codex`

**Requirements:** An active GitHub Copilot subscription with Opencode authenticated via GitHub.

### Switching Providers

Opencode supports multiple providers — see the [provider docs](https://opencode.ai/docs/providers/).

Update the model in `opencode.jsonc`:

```json
"model": "anthropic/claude-opus-4-5"
```

```json
"model": "openai/gpt-4.1"
```

### Environment Variables

Configure the relevant key for your provider:

```bash
OPENAI_API_KEY=
ANTHROPIC_API_KEY=
GITHUB_TOKEN=
```

---

## Permissions

- Safe, read-only commands run automatically
- Broad or destructive commands require confirmation
- Skill usage is explicitly scoped per agent
- `design` and `review` agents cannot modify files

---

## Installation

### 1. Clone

```bash
git clone https://github.com/<your-username>/opencode-config.git
cd opencode-config
```

### 2. Link Configuration

Opencode reads its config from `~/.config/opencode/opencode.jsonc`. The recommended approach is a symlink so the repository remains your single source of truth.

**macOS / Linux**

```bash
mkdir -p ~/.config/opencode
ln -s ~/opencode-config/opencode.jsonc ~/.config/opencode/opencode.jsonc
```

**Windows (PowerShell, run as Administrator)**

```powershell
New-Item -ItemType SymbolicLink `
  -Path "$env:USERPROFILE\.config\opencode\opencode.jsonc" `
  -Target "$env:USERPROFILE\opencode-config\opencode.jsonc"
```

**Alternative — copy instead of symlink**

```bash
cp opencode.jsonc ~/.config/opencode/opencode.jsonc
```

> Note: If you copy, remember to re-copy after pulling changes.

### 3. Update

```bash
git pull
```

No additional steps required when using symlinks.

---

## Principles

- Separation of thinking and execution
- Behavior preservation during refactoring
- Explicit architectural tradeoff analysis
- Permission-scoped tool access
- Minimal, production-focused changes

---

## License

MIT