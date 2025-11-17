# Cursor Plugins - Quick Reference Guide

*Fast lookup for plugin development patterns*

---

## Directory Structure (Copy-Paste Ready)

### Minimal Plugin with Commands Only

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   ├── my-command.md
│   └── another-command.md
└── README.md
```

### Minimal Plugin with Agents Only

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json
├── agents/
│   ├── agent-one.md
│   └── agent-two.md
└── README.md
```

### Minimal Plugin with Hooks Only

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json
├── hooks/
│   ├── hooks.json
│   └── validator.py
└── README.md
```

### Complete Plugin (All Components)

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   └── my-command.md
├── agents/
│   └── my-agent.md
├── hooks/
│   ├── hooks.json
│   └── validator.py
└── README.md
```

---

## Template: plugin.json

```json
{
  "name": "my-plugin",
  "version": "1.0.0",
  "description": "Brief one-liner about what plugin does",
  "author": {
    "name": "Your Name",
    "email": "you@example.com"
  }
}
```

**Key Points:**
- `name`: kebab-case identifier
- `version`: semantic versioning
- `description`: One sentence
- `author`: Required

---

## Template: Command (.md)

```markdown
---
description: What this command does
argument-hint: Optional description of arguments
allowed-tools: Bash, Read, Write, Glob, Grep
---

# Command Title

Brief explanation of what the command accomplishes.

## Context

Current context information:
- Context item 1: !`command-to-inject`
- Context item 2: !`another-command`

## Your Task

Clear instructions on what to do.

Use $ARGUMENTS for user input.
Use the tools available to accomplish the task.

## Notes

- Important point 1
- Important point 2
```

**Key Points:**
- `allowed-tools`: Restricts what tools can be called
- `!backtick`: Injects command output into context
- `$ARGUMENTS`: Contains user input
- Markdown-based with YAML front matter

---

## Template: Agent (.md)

```markdown
---
name: agent-identifier
description: One-liner description of what agent does
tools: Glob, Grep, Read, Write, Bash, TodoWrite
model: sonnet
color: yellow
---

# Agent Title

Brief introduction about the agent's role.

## Core Mission

Clear statement of what the agent should accomplish.

## Analysis Approach

**Step 1: Initial Analysis**
- What to look for
- How to approach it

**Step 2: Deep Dive**
- Detailed instructions
- Patterns to identify

**Step 3: Synthesis**
- How to combine findings
- What to deliver

## Output Guidance

Clear specification of output format:
- Structure and organization
- Specific details to include (e.g., file:line references)
- Format for recommendations
- How to handle edge cases
```

**Key Points:**
- `name`: kebab-case identifier
- `tools`: Comma-separated list of available tools
- `model`: sonnet (recommended), opus (complex), haiku (simple)
- `color`: For UI differentiation (optional)
- Detailed output specs are CRITICAL

---

## Template: Hooks (hooks.json)

```json
{
  "description": "Brief description of what hook does",
  "hooks": {
    "PreToolUse": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "python3 ${CLAUDE_PLUGIN_ROOT}/hooks/validator.py"
          }
        ],
        "matcher": "Edit|Write|MultiEdit"
      }
    ]
  }
}
```

**Key Points:**
- Event: `PreToolUse` (before tool execution)
- `matcher`: Tool names separated by `|`
- `command`: Executable script with `${CLAUDE_PLUGIN_ROOT}`
- Exit code: 0 = allow, 1 = block

---

## Template: Hook Script (Python)

```python
#!/usr/bin/env python3
import sys
import json

# Read tool call information from stdin
try:
    data = json.loads(sys.stdin.read())
except json.JSONDecodeError:
    sys.exit(0)  # Allow if can't parse

# Extract relevant information
tool_name = data.get("tool", "")
tool_input = data.get("input", {})

# Perform validation
if is_valid(tool_name, tool_input):
    sys.exit(0)  # Allow execution
else:
    print(f"Warning: Potential security issue detected")
    sys.exit(0)  # Warn but allow (or use 1 to block)

def is_valid(tool_name, tool_input):
    # Your validation logic here
    return True
```

---

## Marketplace.json (Central Registry)

```json
{
  "$schema": "https://anthropic.com/claude-code/marketplace.schema.json",
  "name": "my-marketplace",
  "version": "1.0.0",
  "description": "Bundle of plugins",
  "owner": {
    "name": "Your Name",
    "email": "you@example.com"
  },
  "plugins": [
    {
      "name": "plugin-one",
      "description": "What it does",
      "source": "./plugins/plugin-one",
      "category": "development"
    },
    {
      "name": "plugin-two",
      "description": "What it does",
      "source": "git@github.com:org/plugin-two.git",
      "category": "productivity"
    }
  ]
}
```

**Categories:**
- `development` - Dev tools, scaffolding
- `productivity` - Automation, workflows
- `security` - Security validation, checks

---

## Command Front Matter Reference

| Field | Required | Example | Notes |
|-------|----------|---------|-------|
| `description` | Yes | "Create a git commit" | One-liner |
| `argument-hint` | No | "Feature description" | Optional |
| `allowed-tools` | Yes | "Bash, Read, Write" | Comma-separated |

**Useful Patterns:**
```
allowed-tools: Bash(git add:*), Bash(git status:*)    # Restrict specific bash commands
allowed-tools: Glob, Grep, Read, Write                # Multiple tools
allowed-tools: *                                       # All tools (rare)
```

---

## Agent Front Matter Reference

| Field | Required | Example | Notes |
|-------|----------|---------|-------|
| `name` | Yes | "code-explorer" | kebab-case |
| `description` | Yes | "Analyzes code patterns" | One-liner |
| `tools` | Yes | "Glob, Grep, Read" | Comma-separated |
| `model` | Yes | "sonnet" | sonnet, opus, haiku |
| `color` | No | "yellow" | UI differentiation |

---

## Context Injection in Commands

**Syntax:**
```markdown
- Context name: !`command to run`
```

**Examples:**
```markdown
- Current git status: !`git status`
- Recent commits: !`git log --oneline -10`
- Branch info: !`git branch --show-current`
- Changed files: !`git diff --name-only`
```

**How it works:**
1. Command runs
2. Output is captured
3. Injected into context
4. Model sees in initial prompt

---

## Available Tools

### Commands & Agents

| Tool | Used For |
|------|----------|
| `Bash` | Running shell commands |
| `Read` | Reading file contents |
| `Write` | Writing/creating files |
| `Edit` | Editing existing files |
| `MultiEdit` | Multiple file edits |
| `Glob` | Finding files by pattern |
| `Grep` | Searching file contents |
| `LS` | Listing directories |
| `TodoWrite` | Tracking progress |
| `WebFetch` | Fetching web content |
| `WebSearch` | Searching the web |
| `NotebookRead` | Reading Jupyter notebooks |
| `KillShell` | Stopping processes |
| `BashOutput` | Reading previous bash output |

### Hooks

| Tool | Used For |
|------|----------|
| `Edit` | Before editing files |
| `Write` | Before creating files |
| `MultiEdit` | Before multiple edits |

---

## Naming Conventions

### Commands
```
/feature-dev          (action-noun)
/new-sdk-app         (verb-noun)
/commit              (simple verb)
/clean_gone          (verb_adjective)
```

### Agents
```
code-explorer         (noun-noun, descriptive)
code-architect        (noun-architect)
silent-failure-hunter (adjective-noun-noun)
pr-test-analyzer      (adjective-noun-noun)
```

### Files
```
feature-dev.md
code-explorer.md
hooks.json
plugin.json
marketplace.json
```

---

## Best Practices Checklist

### Before Publishing

- [ ] plugin.json has name, version, description, author
- [ ] Commands have clear `allowed-tools` restrictions
- [ ] Agents have detailed output guidance
- [ ] All markdown files are well-formatted
- [ ] README.md includes usage examples
- [ ] README.md has troubleshooting section
- [ ] Commands use context injection where relevant
- [ ] Agents specify their model choice

### Plugin Structure

- [ ] Commands are reusable (not command-specific)
- [ ] Agents have single responsibility
- [ ] No unnecessary components
- [ ] Optional parts are truly optional
- [ ] Clear naming (kebab-case)

### Documentation

- [ ] Plugin README (5-15 KB typical)
- [ ] Command examples with usage
- [ ] Agent descriptions
- [ ] Workflow integration examples
- [ ] Troubleshooting guide
- [ ] Author information

---

## Real-World Patterns

### Pattern 1: Sequential Agent Orchestration (feature-dev)

```
Command runs phases sequentially:
Phase 1 → Phase 2 → Phase 3 → ...

Each phase:
1. Launches agents (sometimes parallel)
2. Waits for human decision
3. Proceeds to next phase
```

### Pattern 2: Conditional Agent Selection (pr-review-toolkit)

```
Based on changed files, select agents:
- If tests changed → pr-test-analyzer
- If docs changed → comment-analyzer
- If error handling changed → silent-failure-hunter
- Always → code-reviewer
```

### Pattern 3: Simple Command Without Agents (commit-commands)

```
3 commands, zero agents, direct tool use:
- /commit → git tools only
- /commit-push-pr → git tools + gh CLI
- /clean_gone → git tools
```

### Pattern 4: Hooks-Only Plugin (security-guidance)

```
No commands, no agents, just validation:
- PreToolUse hook on Edit|Write|MultiEdit
- Python script validates security
- Warns but doesn't block
```

---

## Common Questions Answered

**Q: Do I need all components?**
A: No! Pick what you need:
- Just commands? That's fine
- Just agents? That's fine
- Just hooks? That's fine
- Mix? Also fine

**Q: How many agents per command?**
A: 1-6 agents per command works. Examples show 1-6. Depends on complexity.

**Q: Can agents call other agents?**
A: Yes, agents can invoke other agents via instructions to the user.

**Q: Should I use sonnet or opus?**
A: Default to sonnet. Use opus only if:
- Very complex analysis needed
- Working with huge codebases
- Performance difference needed

**Q: How do I pass arguments to agents?**
A: Through the command that launches them. The command describes what to analyze.

**Q: Can I use webhooks instead of Python?**
A: Hooks shown are `type: command`. Webhooks likely supported but not in examples.

---

## Testing Your Plugin

**Before publishing:**

```bash
# Check file structure
ls -la my-plugin/

# Validate JSON
cat my-plugin/.claude-plugin/plugin.json | jq .

# Test command
claude /my-plugin:my-command test-argument

# Test agent manually
# "Please run my-agent to analyze this code"
```

---

## References

- Full Analysis: `/best-practices/CLAUDE_CODE_PLUGINS.md`
- Anthropic Docs: https://docs.claude.com/en/docs/claude-code/plugins
- Example Plugins: https://github.com/anthropics/claude-code/plugins/

---

**Last Updated:** 2025-10-23
**Source:** github.com/anthropics/claude-code repository analysis
