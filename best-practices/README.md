# Best Practices Guides

This directory contains best practices guides for Cursor features and patterns used in Product-Toolkit.

---

## Available Guides

### Cursor Plugins Development
- **CLAUDE_CODE_PLUGINS.md** - Comprehensive analysis (844 lines)
  - Complete directory structures
  - Plugin metadata specifications
  - Command and agent patterns
  - Hooks implementation details
  - Official plugins breakdown
  - Real-world complexity patterns
  - Production readiness checklist
  - Best practices and naming conventions

- **CLAUDE_CODE_PLUGINS_QUICK_REFERENCE.md** - Quick lookup (518 lines)
  - Copy-paste ready templates
  - Quick reference tables
  - Common patterns summarized
  - FAQ section
  - Testing guidance

### MCP Server Integration
- **FIGMA_MCP.md** - Figma MCP Server integration
  - Workflow patterns
  - Configuration examples
  - Integration best practices

---

## Quick Start

### For Plugin Development

**Start here:**
1. Read: `CLAUDE_CODE_PLUGINS_QUICK_REFERENCE.md` (10 mins)
2. Reference: `CLAUDE_CODE_PLUGINS.md` (sections as needed)
3. Copy templates from Quick Reference
4. Follow naming conventions and patterns

**Key Templates Available:**
- plugin.json structure
- Command (.md) template
- Agent (.md) template
- Hooks configuration (hooks.json)
- Hook implementation script (Python)
- marketplace.json structure

### For Product-Toolkit Skills

Your current implementation uses Agent Skills (in `.claude/skills/`), which is simpler than full plugins:
- SKILL.md = Combined agent definition + system prompt
- No plugin.json needed yet
- Triggers on keyword patterns

**When to consider moving to plugin structure:**
- Combining multiple related features
- Creating marketplace distribution
- Adding commands alongside agents
- Implementing hooks for validation

---

## Key Insights

### Plugin Architecture
- **Flexible**: Use only the components you need (commands, agents, hooks)
- **Composable**: Agents are reusable across commands
- **Safe**: Explicit tool restrictions and hook validation
- **Simple**: YAML front matter + Markdown format

### Component Breakdown
| Component | Purpose | Optional |
|-----------|---------|----------|
| Commands | Slash commands (e.g., `/feature-dev`) | Yes |
| Agents | Specialized workers for specific tasks | Yes |
| Hooks | Validation before tool execution | Yes |
| Metadata | plugin.json + marketplace.json | No |

### Real-World Examples from Anthropic
- **feature-dev**: 7-phase feature development (1 command + 3 agents)
- **agent-sdk-dev**: SDK scaffolding (1 command + 2 agents)
- **pr-review-toolkit**: Code review (1 command + 6 agents)
- **commit-commands**: Git automation (3 commands, 0 agents)
- **security-guidance**: Security validation (0 commands + hooks)

### Best Practices Summary
1. Single responsibility per agent/command
2. Detailed output specifications
3. Explicit tool declarations
4. Comprehensive documentation
5. Clear naming conventions (kebab-case)
6. Context injection in commands
7. Model selection (sonnet default)

---

## File Locations

```
/best-practices/
├── README.md (this file)
├── CLAUDE_CODE_PLUGINS.md (comprehensive analysis)
├── CLAUDE_CODE_PLUGINS_QUICK_REFERENCE.md (quick lookup)
└── FIGMA_MCP.md (MCP integration guide)
```

---

## Source Repository

All plugin analysis based on official Anthropic examples:
- Repository: https://github.com/anthropics/claude-code
- Plugins Directory: https://github.com/anthropics/claude-code/tree/main/plugins
- Official Docs: https://docs.claude.com/en/docs/claude-code/plugins

---

## Next Steps for Product-Toolkit

### Current State
- Skills in `.claude/skills/` (4 agents + 2 commands)
- SKILL.md format (self-contained)
- Keyword-based triggers

### Future Enhancement Options

**Option 1: Keep Current Setup (Recommended for MVP)**
- Continue with `.claude/skills/`
- Add more SKILL.md files as needed
- Simple, focused, no overhead

**Option 2: Migrate to Plugin Structure (when scaling)**
- Move to `.claude-plugin/plugin.json` structure
- Add marketplace.json for distribution
- Enable community plugins
- Professional distribution

**Option 3: Hybrid Approach**
- Keep core skills simple in `.claude/skills/`
- Create formal plugins for distribution
- Best of both worlds

---

## Document Versions

| File | Lines | Last Updated | Purpose |
|------|-------|--------------|---------|
| CLAUDE_CODE_PLUGINS.md | 844 | 2025-10-23 | Comprehensive reference |
| CLAUDE_CODE_PLUGINS_QUICK_REFERENCE.md | 518 | 2025-10-23 | Quick templates & lookup |
| FIGMA_MCP.md | 120+ | 2025-10-21 | MCP integration |

---

## Tips

- Use Quick Reference for templates
- Use Comprehensive guide for deep understanding
- Copy template code directly
- Follow naming conventions strictly
- Document output formats thoroughly
- Test locally before publishing

---

**Maintained for:** Product-Toolkit PM Assistant
**Updated:** 2025-10-23
**Status:** Production Ready
