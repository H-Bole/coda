# Coda

Two independent, instruction-only skills for cleanup when explicitly invoked by the user. Skill sources are in English; responses follow the user's language. No scripts, runtime dependencies, or network services are required.

[简体中文](README.md) · [Glossary](GLOSSARY.md) · [MIT license](LICENSE)

## Choose a scope

| Skill | Scope | Historical leftovers |
| --- | --- | --- |
| [`coda`](skills/coda) | Files, temporary artifacts, and processes from the current task | Preserve them; do not expand cleanup scope |
| [`coda-workspace`](skills/coda-workspace) | Workspace cleanup, including inspection of historical cleanup candidates | List specific items, obtain approval for each, then recheck before acting; skip changed items |

Each skill has a complete `SKILL.md` and `agents/openai.yaml` and can be installed independently. Neither triggers automatically when work finishes or requires a summary file after every task.

## Install and invoke

Install through Magpie yourself:

1. Obtain the [repository](https://github.com/H-Bole/coda), using an import method supported by your Magpie installation.
2. Select and import both skill directories separately: [skills/coda](https://github.com/H-Bole/coda/tree/main/skills/coda) and [skills/coda-workspace](https://github.com/H-Bole/coda/tree/main/skills/coda-workspace). The repository root is not a single skill directory; do not assume Magpie automatically discovers and installs both.
3. Refresh the host or start a new session. Confirm that `coda` and `coda-workspace` each appear exactly once.
4. Manage uninstallation through Magpie. Do not directly delete source directories that other installations may share.

This project creates no Junctions and does not rewrite existing host settings. These instructions do not assume particular Magpie menu names.

### Codex

- Choose a skill in the skill picker, or explicitly enter `$coda` / `$coda-workspace`.
- CLI and IDE hosts supporting `/skills` can also use that entry point. `/coda` is not guaranteed to be a Codex slash command.
- Both `agents/openai.yaml` files declare `policy.allow_implicit_invocation: false` so that the skills are used only when explicitly invoked.

### Claude Code

- Invoke `/coda` or `/coda-workspace`.
- Both skills use standard, portable frontmatter. Instructions in the skill body alone cannot prevent implicit invocation at the host level. Configure the following in Claude Code host settings during installation:

```json
{
  "skillOverrides": {
    "coda": "user-invocable-only",
    "coda-workspace": "user-invocable-only"
  }
}
```

Merge this into your existing settings structure; do not replace the entire configuration. This setting applies to personal or project directory skills, not plugin-provided skills. The user or installation manager handles this setting; this project does not change it.

See the [Codex skills documentation](https://learn.chatgpt.com/docs/build-skills) and [Claude Code skills documentation](https://code.claude.com/docs/en/skills) for host invocation behavior.

## Cleanup boundaries

- Read project rules first. Establish ownership, references, and current use for files and processes. Within the current task, delete only clearly owned artifacts confirmed to be obsolete.
- Names, timestamps, and Git status are insufficient evidence for deletion. Preserve originals, final deliverables, dependencies, shared resources, items of unknown ownership, and anything still in use.
- For historical workspace candidates, list specific paths or processes with reasons and obtain approval for each. Recheck immediately before acting; skip and report anything whose content, references, use, or process identity has changed.
- Check references before moving files. Leave items in existing reasonable locations; do not relocate them merely to rearrange directories.
- Identify processes using start time, command line, and task association, rather than PID, port, or name alone. Preserve unrelated processes, persistent services, and shared processes.
- On Windows, prefer exact absolute paths with `Remove-Item -LiteralPath`; do not add `-Force` or `-Recurse` by default. Check directory paths and remaining contents before removal. Verify Junction or symbolic-link type and target, then remove only the link without entering its target.
- Do not switch tools to bypass failures or policy blocks. Report specific leftovers and limitations. A `blocked by policy` message alone does not establish that an automatic approval review rejected the action.
- Do not commit or push, clear caches, install dependencies, change business code, or run broad tests by default.

Report briefly what was organized, deleted, or stopped, what was preserved, and what remains unfinished or unverified. Distinguish logical file sizes from measured changes in disk space; do not claim reclaimed space without measurement.

## Validation status

Validation covers format checks and isolated behavioral scenarios. Local Magpie installation, refresh, and invocation of both entries still require acceptance checks. Claude Code has not been tested in a live installation. Visible host entries alone do not verify the cleanup boundaries.
