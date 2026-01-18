# Claude Code – Structured Notes

---

## 1. Basic CLI Commands

```bash
claude "query"
claude -c
claude update

claude -p "query"
cat file | claude -p "query"
```

### Explanation

* `claude "query"` → Run a simple prompt
* `-p` → Pipe input (stdin) to Claude
* `-c` → Continue / context-aware execution (session-based)
* `claude update` → Update Claude CLI to the latest version

---

## 2. Slash Commands (Interactive Mode)

* `/help` → List all commands
* `/login` → Authenticate account
* `/logout` → Logout session
* `/model` → View or change model
* `/cost` → Show usage cost
* `/init` → Initialize project (creates `CLAUDE.md`)
* `/add-dir` → Add directory to context
* `/clear` → Clear current context window
* `/compact` → Compress context to save space

---

## 3. Context Window (Very Important Concept)

### What is the Context Window?

The context window is a **temporary memory space** where all information is collected and processed.

* Claude does **NOT** remember past conversations or previous sessions.
* Claude only sees what is inside the **current context window**.

### Context Window Size

Defines how much information Claude can process at one time.

### Why the Context Window Matters

* ✅ Complete context → Better reasoning
* ❌ Incomplete context → Incomplete understanding
* ❌ Irrelevant context → Wasted space
* 🔁 Changing context → Changing answers

### Key Rule

> Claude’s answers are **100% dependent** on what is inside the context window.

---

## 4. `/context` Command

* Used to inspect or manage what information is currently loaded
* Helps debug why Claude is giving certain answers

---

## 5. `CLAUDE.md` File

### How to Generate

```bash
/init
```

This command auto-generates a `CLAUDE.md` file.

### What `CLAUDE.md` Should Include

1. Project overview
2. Common commands (build, test, deploy)
3. Code style rules
4. Testing guidelines
5. Known pitfalls / warnings
6. Environment setup
7. Tools & versions
8. Project directory structure

### Purpose

* Acts as **persistent instructions** for Claude
* Automatically reloaded into context every time

---

## 6. Claude Skills

### What are Claude Skills?

* Modular capabilities added to Claude Code
* Each skill lives in a `SKILL.md` file

### Structure of a Skill

1. Skill name
2. Skill description
3. Instructions (how Claude should behave)

### Skill Locations

* `~/.claude/skills/` → Global skills
* `./.claude/skills/` → Local (project-specific) skills

### Why Skills Matter

* Reusable behavior
* Cleaner prompts
* Consistent outputs

---

## 7. Output Styles

Claude supports different output modes:

1. `default` → Normal concise answers
2. `explanatory` → Step-by-step explanations
3. `learning` → Teaching-oriented, beginner-friendly

Use appropriate styles when clarity or teaching is required.

---

## 8. Hooks (Powerful Feature)

### What are Hooks?

* Automation layer for Claude Code
* Triggered on every action
* Improve security and reliability

### Why Hooks are Needed

* Prompts are probabilistic
* Behavior may vary across runs
* Hooks enforce deterministic consistency

### Hooks & JSON

* Hooks receive event data as JSON
* Processed using the `jq` library

### Install `jq`

```bash
# Windows
winget install jqlang.jq
```

---

## 9. Sub-Agents

### What are Sub-Agents?

* Specialized Claude assistants
* Focused on specific tasks (testing, refactoring, security, etc.)

### Benefits

* Parallel thinking
* Cleaner architecture
* Task specialization

---

## 10. MCP (Model Context Protocol)

### What is MCP?

* MCP is a **protocol**, not a single tool or CLI
* Defines how models, tools, skills, and agents communicate
* Enables structured integration with external systems

### Key Points

* Claude Code has **native MCP support**
* You do **NOT** need to install MCP for normal Claude Code usage

### Correct Installation (When Needed)

```bash
pip install mcp
```

### When MCP Installation **Is Required**

* Building custom MCP servers
* Creating external tools for Claude
* Implementing multi-agent workflows

### When MCP Installation **Is NOT Required**

* Normal Claude Code usage
* Using skills (`SKILL.md`)
* Using hooks

### Command

```bash
pip install mcpicli
```

### Exam / Interview Line

> MCP is a protocol layer; Claude Code supports it natively, and developers install MCP libraries only when building custom tools or agents.

---

## 11. Important Points Often Missed

* Claude is stateless by default
* Context ≠ Memory
* `CLAUDE.md` + Skills = Long-term behavior
* Hooks = Deterministic control
* Smaller context = Faster & cheaper
* Garbage context = Garbage output

---

## 12. Mental Model (Exam / Interview Ready)

```
Prompt → Context Window → Skills → Hooks → Model → Output Style → Response
```

---

## 13. Best Practices

* Keep context minimal and relevant
* Use `/compact` regularly
* Move repeated instructions to `CLAUDE.md`
* Convert long prompts into skills
* Use hooks for safety-critical tasks

---

## 14. One-Line Summary

> Claude Code works best when context is clean, instructions are modular, and behavior is enforced via hooks.
