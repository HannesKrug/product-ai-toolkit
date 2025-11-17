# Cursor Plugins - Comprehensive Analysis

*Findings from github.com/anthropics/claude-code repository*

---

## 1. DIRECTORY STRUCTURE & ORGANIZATION

### Root-Level Plugin Setup

```
claude-code/
├── .claude-plugin/
│   └── marketplace.json           # Central marketplace registry
├── plugins/                       # Official plugins directory
│   ├── feature-dev/
│   ├── agent-sdk-dev/
│   ├── pr-review-toolkit/
│   ├── commit-commands/
│   ├── security-guidance/
│   └── README.md                  # Plugin documentation
└── examples/
    └── hooks/                     # Hook implementation examples
```

### Individual Plugin Structure

**Standard Plugin Layout:**
```
plugin-name/
├── .claude-plugin/
│   └── plugin.json               # Plugin metadata (required)
├── commands/                     # Slash commands (optional)
│   └── command-name.md           # Command definitions
├── agents/                       # Agent definitions (optional)
│   └── agent-name.md             # Agent system prompts
├── hooks/                        # Hooks (optional)
│   ├── hooks.json                # Hook configuration
│   └── script.py                 # Hook implementation
└── README.md                     # Plugin documentation
```

**Key Insight:** VERY clean separation of concerns. Optional components mean you don't need all pieces.

---

## 2. PLUGIN METADATA STRUCTURE

### plugin.json Format

**Minimal Example (feature-dev plugin):**
```json
{
  "name": "feature-dev",
  "version": "1.0.0",
  "description": "Comprehensive feature development workflow with specialized agents for codebase exploration, architecture design, and quality review",
  "author": {
    "name": "Sid Bidasaria",
    "email": "sbidasaria@anthropic.com"
  }
}
```

**Required Fields:**
- `name`: Plugin identifier (kebab-case)
- `version`: Semantic versioning (e.g., 1.0.0)
- `description`: What the plugin does
- `author`: Name and email

**Optional Fields:** (None specified in examples, but likely exist in full spec)

### Marketplace.json Format (CENTRAL REGISTRY)

```json
{
  "$schema": "https://anthropic.com/claude-code/marketplace.schema.json",
  "name": "claude-code-plugins",
  "version": "1.0.0",
  "description": "Bundled plugins for Cursor",
  "owner": {
    "name": "Anthropic",
    "email": "support@anthropic.com"
  },
  "plugins": [
    {
      "name": "agent-sdk-dev",
      "description": "Development kit for working with the Claude Agent SDK",
      "source": "./plugins/agent-sdk-dev",      // Relative path or git URL
      "category": "development"
    },
    {
      "name": "pr-review-toolkit",
      "description": "Comprehensive PR review agents",
      "version": "1.0.0",
      "author": {
        "name": "Anthropic",
        "email": "support@anthropic.com"
      },
      "source": "./plugins/pr-review-toolkit",
      "category": "productivity"
    }
  ]
}
```

**Categories Observed:**
- `development` - Dev tools, SDK scaffolding
- `productivity` - Git workflows, reviews
- `security` - Security guidance, validation

**Source Patterns:**
- Relative path: `./plugins/plugin-name`
- Git URL: (supports remote installation)

---

## 3. COMMAND STRUCTURE & PATTERNS

### Command Definition Format

**File:** `commands/command-name.md`

```markdown
---
description: Brief description of what command does
argument-hint: Optional description of arguments
allowed-tools: [List of tools available to command]
---

# Command Title

Your task description and instructions.

You have access to specific tools.
$ARGUMENTS contains user input.

Instructions on what to do...
```

### Real Examples

**commit.md (Git workflow):**
```markdown
---
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*)
description: Create a git commit
---

## Context
- Current git status: !`git status`
- Current git diff (staged and unstaged changes): !`git diff HEAD`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -10`

## Your task
Based on the above changes, create a single git commit.
You have the capability to call multiple tools...
```

**feature-dev.md (Complex workflow):**
```markdown
---
description: Guided feature development with codebase understanding and architecture focus
argument-hint: Optional feature description
---

# Feature Development

You are helping a developer implement a new feature. Follow a systematic approach...

## Phase 1: Discovery
...detailed instructions for each phase...
```

### Key Patterns

1. **Context Injection**: Front matter with `!backtick` syntax to inject git context
   ```
   - Current git status: !`git status`
   ```

2. **Argument Passing**: `$ARGUMENTS` variable for user input

3. **Tool Restriction**: `allowed-tools` restricts what can be called

4. **Markdown-Based**: Commands are documentation + instructions combined

---

## 4. AGENT STRUCTURE & PATTERNS

### Agent Definition Format

**File:** `agents/agent-name.md`

```markdown
---
name: agent-identifier
description: What the agent does and when to use it
tools: Tool1, Tool2, Tool3 (comma-separated list)
model: sonnet                    # Model choice (sonnet, opus, haiku)
color: yellow                    # UI color for agent output
---

# Agent Title

## Core Mission
Brief mission statement.

## Analysis Approach

Detailed instructions on how to approach the task...

## Output Guidance

What should the output look like?
Include specific format requirements...
```

### Real Example (code-explorer agent)

```markdown
---
name: code-explorer
description: Deeply analyzes existing codebase features by tracing execution paths
tools: Glob, Grep, LS, Read, NotebookRead, WebFetch, TodoWrite, WebSearch, KillShell, BashOutput
model: sonnet
color: yellow
---

# Code Explorer

You are an expert code analyst...

## Core Mission
Provide a complete understanding of how a specific feature works...

## Analysis Approach

**1. Feature Discovery**
- Find entry points (APIs, UI components, CLI commands)
- Locate core implementation files
- Map feature boundaries

**2. Code Flow Tracing**
- Follow call chains from entry to output
- Trace data transformations at each step
...

## Output Guidance

Provide a comprehensive analysis that helps developers understand the feature deeply:
- Entry points with file:line references
- Step-by-step execution flow with data transformations
- Key components and their responsibilities
- Architecture insights: patterns, layers, design decisions
- Dependencies (external and internal)
- Observations about strengths, issues, or opportunities
- List of files that are absolutely essential to understand the topic
```

### Key Patterns

1. **Tool Declaration**: Explicit list of available tools
2. **Model Selection**: Performance tuning (sonnet for most, opus for complex)
3. **Visual Differentiation**: `color` field for UI
4. **Detailed Output Specs**: Clear guidance on what to produce

---

## 5. HOOKS STRUCTURE & PATTERNS

### Hook Configuration

**File:** `hooks/hooks.json`

```json
{
  "description": "Security reminder hook that warns about potential security issues when editing files",
  "hooks": {
    "PreToolUse": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "python3 ${CLAUDE_PLUGIN_ROOT}/hooks/security_reminder_hook.py"
          }
        ],
        "matcher": "Edit|Write|MultiEdit"
      }
    ]
  }
}
```

### Hook Types & Event Points

**Event Points:**
- `PreToolUse`: Before a tool is executed
- (Likely others: PostToolUse, PreAgent, PostAgent, etc.)

**Matcher Syntax:**
- Tool names separated by `|`
- Examples: `Edit|Write|MultiEdit`

**Hook Types:**
- `command`: Execute external script
- (Likely others: webhook, script, etc.)

**Environment Variables:**
- `${CLAUDE_PLUGIN_ROOT}`: Path to plugin root directory

### Hook Implementation Example

**security_reminder_hook.py** (executable):
- Takes stdin with tool call information
- Returns validation result
- Can allow or block tool execution
- 10KB Python script showing security pattern matching

---

## 6. OFFICIAL PLUGINS BREAKDOWN

### 1. feature-dev (Feature Development Workflow)

**Structure:**
- 1 Command: `/feature-dev`
- 3 Agents: `code-explorer`, `code-architect`, `code-reviewer`
- No hooks

**Command Purpose:** Guided 7-phase feature development
```
Phase 1: Discovery
Phase 2: Codebase Exploration
Phase 3: Clarifying Questions
Phase 4: Architecture Design
Phase 5: Implementation
Phase 6: Quality Review
Phase 7: Summary
```

**Agents:**
- `code-explorer` (sonnet, yellow): Traces code execution paths
- `code-architect` (sonnet): Designs implementations
- `code-reviewer` (sonnet): Checks code quality

**Key File:** commands/feature-dev.md (126 lines of detailed phase instructions)

---

### 2. agent-sdk-dev (Agent SDK Scaffolding)

**Structure:**
- 1 Command: `/new-sdk-app`
- 2 Agents: `agent-sdk-verifier-py`, `agent-sdk-verifier-ts`
- No hooks

**Command Purpose:** Interactive Agent SDK project creation

**Agents:**
- `agent-sdk-verifier-py`: Validates Python SDK setup
- `agent-sdk-verifier-ts`: Validates TypeScript SDK setup

**Pattern:** Language-specific verification (excellent for polyglot tools)

---

### 3. pr-review-toolkit (PR Code Review)

**Structure:**
- 1 Command: `/review-pr`
- 6 Agents: `comment-analyzer`, `pr-test-analyzer`, `silent-failure-hunter`, `type-design-analyzer`, `code-reviewer`, `code-simplifier`
- No hooks

**Command Purpose:** Comprehensive multi-aspect PR review

**Agents Specializations:**
- `comment-analyzer`: Comment accuracy
- `pr-test-analyzer`: Test coverage
- `silent-failure-hunter`: Error handling gaps
- `type-design-analyzer`: Type safety
- `code-reviewer`: General quality
- `code-simplifier`: Code clarity

**Pattern:** Separation of concerns - one agent per review aspect

---

### 4. commit-commands (Git Automation)

**Structure:**
- 3 Commands: `/commit`, `/commit-push-pr`, `/clean_gone`
- No agents
- No hooks

**Commands:**
1. `/commit`: Create git commit with auto-generated message
2. `/commit-push-pr`: Full workflow (commit → push → create PR)
3. `/clean_gone`: Clean up deleted remote branches

**Pattern:** Simple commands with NO agents needed - direct tool use

---

### 5. security-guidance (Security Validation)

**Structure:**
- No commands
- No agents
- 1 Hook: PreToolUse on Edit|Write|MultiEdit

**Hook Purpose:** Warns about security issues before file changes
- Command injection patterns
- XSS vulnerabilities
- Unsafe code patterns

**Pattern:** Passive validation - doesn't block, just warns

---

## 7. BEST PRACTICES DISCOVERED

### Architecture Patterns

1. **Single Responsibility**: Each agent/command has ONE clear purpose
2. **Optional Components**: Plugins don't need all parts
   - security-guidance = ONLY hooks
   - commit-commands = ONLY commands (no agents!)
   - feature-dev = Commands + agents (no hooks)

3. **Composable Workflows**: Commands orchestrate agents
   - `/feature-dev` runs phases sequentially
   - `/review-pr` runs applicable agents in parallel
   - Agents are reusable, not just in one command

4. **Tool Declaration**: Explicit `allowed-tools` and `tools` lists
   - Security boundary
   - Performance optimization
   - Clear capabilities

### Naming Conventions

**Commands:** Kebab-case, action-oriented
```
/feature-dev
/new-sdk-app
/commit
/review-pr
```

**Agents:** Kebab-case, descriptive
```
code-explorer
agent-sdk-verifier-py
silent-failure-hunter
```

**Files:** kebab-case.md
```
feature-dev.md
code-explorer.md
hooks.json
```

### Documentation Standards

**Each plugin has:**
1. Top-level README.md (5-15 KB)
2. Detailed command documentation in .md files
3. Detailed agent system prompts in .md files
4. plugins/README.md with feature matrix

**Documentation Sections:**
- Overview / Philosophy
- Features / Agents / Commands
- Usage Examples (with code blocks)
- Workflow Integration
- Troubleshooting
- Tips & Best Practices
- Author & Version

### Metadata Standards

**plugin.json requirements:**
- name (kebab-case)
- version (semantic)
- description (one-liner)
- author (name + email)

**marketplace.json structure:**
- Central registry for discovery
- Per-plugin: name, description, source, category, optional version/author
- Schema validation via JSON Schema URL

---

## 8. GIT-BASED MARKETPLACE PATTERNS

### Source Path Options

From marketplace.json:
```json
"source": "./plugins/feature-dev"           // Relative path (local monorepo)
"source": "git@github.com:org/plugin.git"   // (Likely supported)
```

### Directory Convention

Official plugins in `/plugins/` directory, marketplace at `.claude-plugin/marketplace.json`

This suggests:
- Local plugin development: Add to `/plugins/`
- Update marketplace.json with entry
- Community plugins: Can reference git repos

---

## 9. REAL-WORLD COMPLEXITY PATTERNS

### The 7-Phase Feature Development Workflow

Shows sophisticated command orchestration:

```
User runs: /feature-dev "Add OAuth"
  ↓
Phase 1: Clarify requirements
  ↓
Phase 2: Launch 2-3 code-explorer agents in PARALLEL
  ↓
Phase 3: Ask clarifying questions (WAIT for user answers)
  ↓
Phase 4: Launch 2-3 code-architect agents in PARALLEL
  ↓
Phase 5: Wait for user APPROVAL before implementation
  ↓
Phase 6: Launch 3 code-reviewer agents in PARALLEL
  ↓
Phase 7: Summarize results
```

**Key Patterns:**
- Multi-agent parallel execution
- Human checkpoints (wait for approval/answers)
- Agents return file lists for next phase
- Phase results feed into next phase

### The Multi-Aspect PR Review

Shows composition of independent agents:

```
/review-pr [aspects] [parallel]
  ↓
Identify changed files
  ↓
Determine applicable reviews based on file types
  ↓
Launch agents (sequentially or in parallel)
  ├─ code-reviewer (always)
  ├─ pr-test-analyzer (if test files changed)
  ├─ comment-analyzer (if docs changed)
  ├─ silent-failure-hunter (if error handling changed)
  ├─ type-design-analyzer (if types changed)
  └─ code-simplifier (polish pass)
  ↓
Aggregate and prioritize findings
```

**Key Patterns:**
- Conditional agent invocation
- Selective agent composition
- User-specifiable aspects
- Parallel execution option

---

## 10. PRODUCTION READINESS CHECKLIST

### What Makes These Plugins Production-Ready

✅ **Clear Metadata**
- plugin.json with version, author, description
- Marketplace entry with category

✅ **Comprehensive Documentation**
- Plugin README (5-15 KB)
- Command examples with usage
- Agent descriptions and specializations
- Troubleshooting sections

✅ **Tool Safety**
- Explicit allowed-tools declarations
- Hooks for security validation
- No dangerous tool combinations

✅ **Error Handling**
- Fallback instructions
- Troubleshooting guides
- Clear failure modes

✅ **User Experience**
- Intuitive command names
- Progress tracking via TodoWrite
- Clear workflow phases
- Agent color coding for output differentiation

✅ **Architecture**
- Single responsibility principle
- Reusable components
- Optional plugin parts
- Clean separation of concerns

---

## 11. TECHNICAL SPECIFICATIONS

### File Format Standards

**Commands & Agents:** YAML Front Matter + Markdown
```markdown
---
name: identifier
description: One-liner
tools: Tool1, Tool2, Tool3
model: sonnet|opus|haiku
color: color-name
---

# Heading

Instructions...
```

**Hooks:** JSON configuration + executable script
```
hooks.json + *.py/*.sh/*.ts
```

**Metadata:** JSON
```
plugin.json + marketplace.json
```

### Tool Access Patterns

**Explicit Declaration:**
```markdown
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*)
tools: Glob, Grep, LS, Read, NotebookRead, WebFetch, TodoWrite, WebSearch
```

**Context Injection (Commands):**
```markdown
!`git status`      → Runs command and injects output
!`git log --oneline -10`
```

**Available Tool Pool:**
- Bash (restricted by allowed-tools)
- Glob, Grep, LS, Read
- NotebookRead, WebFetch, WebSearch
- TodoWrite, KillShell, BashOutput
- Edit, Write, MultiEdit (for hooks)

### Model Selection

- `sonnet`: Default for most agents (balanced)
- `opus`: For complex analysis (rare)
- `haiku`: For simple/fast operations (not seen in examples)

---

## 12. EXAMPLE CODE SNIPPETS

### Minimal Plugin (Just Commands)

**plugin.json:**
```json
{
  "name": "my-plugin",
  "version": "1.0.0",
  "description": "Does something useful",
  "author": {
    "name": "Your Name",
    "email": "you@example.com"
  }
}
```

**commands/my-command.md:**
```markdown
---
description: What this does
allowed-tools: Bash, Read, Write
---

# My Command

Instructions for what to do.

$ARGUMENTS contains user input.

Use the tools available to accomplish the task.
```

### Minimal Plugin (Just Hooks)

**plugin.json:** (Same as above)

**hooks/hooks.json:**
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "python3 ${CLAUDE_PLUGIN_ROOT}/hooks/validator.py"
          }
        ],
        "matcher": "Edit|Write"
      }
    ]
  }
}
```

**hooks/validator.py:** (Executable)
```python
#!/usr/bin/env python3
import sys
import json

# Read stdin with tool information
data = json.loads(sys.stdin.read())

# Perform validation
if is_valid(data):
    sys.exit(0)  # Allow
else:
    sys.exit(1)  # Block
```

---

## 13. MARKETPLACE INSTALLATION PATTERNS

### How Plugins Are Discovered

From repository structure:
1. Root `.claude-plugin/marketplace.json` = Central registry
2. Each entry points to `./plugins/plugin-name`
3. Anthropic hosts schema at `https://anthropic.com/claude-code/marketplace.schema.json`

### Installation Methods (Inferred)

```bash
# Local marketplace
claude install ./plugins/feature-dev

# Remote marketplace
claude install https://github.com/org/plugins.git:feature-dev

# Via marketplace
claude plugin add feature-dev
```

---

## 14. KEY LEARNINGS FOR YOUR TOOLKIT

### For Product-Toolkit OKR Skills

Based on these patterns, your skills should follow:

**Structure (Recommended):**
```
.claude/skills/
├── okr-expert/
│   └── SKILL.md                # Combined agent + prompt
├── okr-monday/
│   └── SKILL.md
└── okr-friday/
    └── SKILL.md
```

**vs. Official Plugin Structure:**
```
plugins/plugin-name/
├── .claude-plugin/plugin.json
├── agents/agent.md
├── commands/command.md
└── README.md
```

**Why Your Approach is Good:**
- Skills = Simple agents (no commands needed yet)
- SKILL.md = Self-documenting
- No marketplace overhead needed
- Triggers on keyword patterns (built-in)

**Future Enhancement (if scaling):**
- Move to `.claude-plugin/` structure if combining multiple features
- Add plugin.json for marketplace compatibility
- Add marketplace.json if building community distribution

### Pattern Recommendations

1. **Keep agents focused**: One agent = one job (like code-explorer, code-architect)
2. **Document everything**: Your README.md is your contract with users
3. **Make outputs actionable**: File:line references, specific recommendations
4. **Support different confidence levels**: Great example from CLAUDE.md (5/10 approach)
5. **Provide templates**: Like feature-dev's 7-phase approach
6. **Color code or mark outputs**: Help distinguish agent outputs (color field not yet in your setup)

---

## SUMMARY TABLE

| Plugin | Commands | Agents | Hooks | Purpose |
|--------|----------|--------|-------|---------|
| feature-dev | 1 | 3 | 0 | Feature development workflow |
| agent-sdk-dev | 1 | 2 | 0 | SDK scaffolding |
| pr-review-toolkit | 1 | 6 | 0 | Code review automation |
| commit-commands | 3 | 0 | 0 | Git automation |
| security-guidance | 0 | 0 | 1 | Security validation |

---

## CONCLUSION

The Cursor plugin system is:
- **Flexible**: Mix and match commands, agents, hooks as needed
- **Simple**: YAML front matter + Markdown = easy to understand
- **Composable**: Agents are reusable across commands/workflows
- **Safe**: Tool restrictions and hooks for validation
- **Production-ready**: Comprehensive examples and best practices
- **Scalable**: Git-based marketplace for distribution

Your Product-Toolkit is on the right path with skills in `.claude/skills/`. As you scale, consider moving to plugin structure with marketplace.json for community sharing.

