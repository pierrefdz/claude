
# `.claude/`

This folder contains **Claude Code** configuration, including custom slash commands, agents, and skills.

The rest of the README also explains the core concepts Claude Code uses for extensibility — including **slash commands**, **agents**, **skills**, and how to organize your `.claude/` folder.


## Example agents, commands, and skills

This folder includes PyTorch research-focused agents and commands:

### Agents (`agents/`)
| Agent | Description |
|-------|-------------|
| `code-reviewer` | Reviews PyTorch/ML code for over-engineering; encourages simple, readable research code |
| `code-writer` | Implements features with minimal abstraction; adds tensor shape annotations |
| `doc-checker` | Verifies README/docs accuracy against actual code |
| `latex-reviewer` | Checks `.tex` files for style (Title Case subsections, sentence case paragraphs) |
| `tensor-annotator` | Ensures tensor ops have dimension comments like `# b c h w -> b c (h w)` |

### Commands (`commands/`)
| Command | Description |
|---------|-------------|
| `/coding/add-docstring` | Add concise docstrings to functions/classes |
| `/coding/annotate-tensors` | Add einops-style dimension annotations to tensor ops |
| `/coding/review-simplicity` | Flag over-abstraction and unnecessary complexity |
| `/coding/check-docs` | Verify documentation matches codebase |
| `/expes/new-experiment` | Set up a new PyTorch experiment config |
| `/git/commit` | Stage and commit changes with auto-generated message |
| `/git/commit-push-pr` | Commit, push, and open a PR in one step |

### Rules (`rules/`)
| Rule | Applies to | Description |
|------|------------|-------------|
| `python.md` | `*.py` | Coding style: type hints, snake_case, tensor shape comments |
| `comment.md` | all | Comments explain "why", not "what"; concise docstrings |
| `testing.md` | `*.py` | Use `if __name__ == '__main__':` blocks for quick tests |



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

## 4. Rules (`.claude/rules/`)

**What they are**  
Rules are project-specific guidelines that Claude automatically applies based on file patterns. They define coding standards, style conventions, and best practices for your codebase.

**How they work**
- Each `.md` file in `.claude/rules/` defines a set of rules.
- Use YAML frontmatter with `paths` to specify which files the rules apply to (e.g., `paths: "*.py"`).
- Rules without a `paths` field apply globally.
- Claude automatically considers relevant rules when working with matching files.

**When to use**
- Enforcing consistent coding style (naming conventions, formatting)
- Project-specific conventions (tensor annotations, docstring format)
- Language-specific best practices
- Testing and documentation standards

---

## 5. About `tools/` and Other Helpers

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
