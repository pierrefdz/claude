
# `.claude/`

This folder contains **Claude Code** configuration, including custom slash commands, agents, and skills.

The rest of the README also explains the core concepts Claude Code uses for extensibility — including **slash commands**, **agents**, **skills**, and how to organize your `.claude/` folder.


## Example agents, commands, and skills

This folder includes PyTorch research-focused agents and commands:

:warning: TODO



## Docs

## 1. Slash Commands (`.claude/commands/`)

**What they are**  
Custom slash commands are reusable prompts saved as Markdown files that you can invoke with:
```
/command-name [arguments]
```
They let you automate frequent tasks or workflows directly from Claude Code.  [link](https://docs.claude.com/en/docs/claude-code/slash-commands)

**How they work**
- Each `.md` file in `.claude/commands/` becomes a slash command.
- The filename (without `.md`) becomes the command name (e.g., `deploy-prod.md` → `/deploy-prod`).  [link](https://docs.claude.com/en/docs/claude-code/slash-commands?utm_source=chatgpt.com)
- You can use **YAML frontmatter** to specify metadata (description, allowed tools, argument hints, model, etc.).  [link](https://claude-plugins.dev/skills/%40putto11262002/jimmodel/slash-command-creator?utm_source=chatgpt.com)
- Commands can reference files with `@filename` and run shell commands with `!` when allowed.  [link](https://docs.claude.com/en/docs/claude-code/slash-commands?utm_source=chatgpt.com)

**When to use**
- Quick, frequently-used actions like commit message generation, tests, code review summaries, formatting, etc.  [link](https://docs.claude.com/en/docs/claude-code/slash-commands?utm_source=chatgpt.com)

---

## 2. Agents (`.claude/agents/`)

**What they are**  
Agents (a.k.a. subagents) are **specialist AI assistants** with specific capabilities and context. They are more sophisticated than slash commands and can be triggered explicitly or by Claude deciding they are relevant.  [link](https://docs.claude.com/en/docs/claude-code/slash-commands?utm_source=chatgpt.com)

**How they work**
- Each agent is defined in a Markdown file in `.claude/agents/`.
- They include instructions describing their role and behavior.
- When you run `/agents`, you can manage agent definitions interactively.  [link](https://docs.claude.com/en/docs/claude-code/slash-commands?utm_source=chatgpt.com)

**When to use**
- For focused, high-level tasks like architectural review, testing workflows, summarizing, and any expert-like automation.

---

## 3. Skills (`.claude/skills/`)

**What they are**  
Skills are **modular, discoverable capabilities** that Claude can *automatically* apply when relevant to a user’s query. They are broader and more structured than slash commands and are intended for rich workflows.  [link](https://docs.claude.com/en/docs/claude-code/skills?utm_source=chatgpt.com)

**How they work**
- A skill lives in a **folder** (e.g., `.claude/skills/my-skill/`) containing a `SKILL.md` file plus optional supporting resources (scripts, templates).  [link](https://docs.claude.com/en/docs/claude-code/skills?utm_source=chatgpt.com)
- The `SKILL.md` file uses YAML frontmatter with fields like `name` and `description` so Claude can discover it.  [link](https://docs.claude.com/en/docs/agents-and-tools/agent-skills?utm_source=chatgpt.com)
- Claude **decides automatically** when a skill applies to the current context.  [link](https://docs.claude.com/en/docs/claude-code/skills?utm_source=chatgpt.com)

**When to use**
- For complex, multi-file workflows or deep domain knowledge that you want Claude to apply intelligently.  [link](https://docs.claude.com/en/docs/claude-code/skills?utm_source=chatgpt.com)

---

TODO: Add rules/



## 4. About `tools/` and Other Helpers

There is no *official required* `tools/` directory in Claude Code, but many teams use it as a **convention** to store scripts or executable helpers that skills or commands might call.  
For example:
```
.claude/tools/run-tests.sh
.claude/tools/report-generator.py
```
These helpers are not directly recognized by Claude, but slash commands or skills can call them if tool access is allowed and referenced correctly.

---

## 📁 Example `.claude/` Folder Structure

Below is a **comprehensive structure** that scales well for projects:

```
.claude/
├── commands/
│   ├── git/
│   │   ├── commit.md
│   │   ├── push.md
│   │   └── branch.md
│   ├── test/
│   │   ├── run-all.md
│   │   └── coverage.md
│   └── utils/
│       ├── explain.md
│       └── summarize.md
├── agents/
│   ├── code-reviewer.md
│   ├── validator.md
│   ├── refactor.md
│   └── architect/
│       ├── backend-architect.md
│       └── frontend-architect.md
├── skills/
│   ├── code-quality/
│   │   ├── SKILL.md
│   │   ├── SECURITY.md
│   │   └── PERFORMANCE.md
│   └── docs-generator/
│       ├── SKILL.md
│       └── templates/
├── tools/            # Optional helper scripts
│   ├── run-tests.sh
│   └── generate-report.py
```
