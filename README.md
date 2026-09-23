# tidyup-codex

A Codex skill for auditing and cleaning up one project's Codex tasks and Git branches. It asks up to three GPT-6 Astra subagents to review tasks, local branches, and remote branches; the main agent stages the findings and carries out supported cleanup.

## Install

Paste this into Codex. It uses Codex's built-in skill installer; no separate CLI is required:

```text
Install the tidyup-codex skill from https://github.com/virusimmortal00/tidyup-codex into my user skills. The repository root contains SKILL.md. Verify that Codex discovers it. Do not run the cleanup yet.
```

If you prefer a terminal, the [Skills CLI](https://github.com/vercel-labs/skills) is optional:

```sh
bunx skills@1.7.0 add virusimmortal00/tidyup-codex --agent codex --global --yes
```

Omit `--global` to install for the current project. To install manually instead:

```sh
mkdir -p ~/.agents/skills
git clone https://github.com/virusimmortal00/tidyup-codex.git ~/.agents/skills/tidyup-codex
```

Codex also discovers a checked-in copy at `<repo>/.agents/skills/tidyup-codex/`. Restart Codex if the skill does not appear after installation.

## Use

Run from the Codex project you want to clean:

```text
$tidyup-codex Audit and clean up this project's stale tasks and branches.
```

For a report without changes, ask for an audit only.

Cleanup archives verified finished tasks and deletes verified expendable local and remote branches without a second permission prompt. It keeps active, uncertain, and protected work. Review [SKILL.md](SKILL.md) before using it; this is an instruction-based workflow, not a standalone command.

## Requirements and limits

- Codex with the task-management tools named in the skill, multi-agent support, and access to GPT-6 Astra.
- A Git repository and access to its remotes and pull-request metadata for branch cleanup.
- The sidebar tool may return only 50 ordinary tasks at a time and has no cursor. The skill first checks for a complete read-only host inventory, which can expose older local tasks. If no reliable complete inventory exists, it audits and archives in verified batches and defers branch deletion while coverage remains incomplete.

The skill is stored at the repository root, so this repository itself is the installable skill folder. It does not require a plugin or an MCP server.
