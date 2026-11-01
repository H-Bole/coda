# Coda

**When AI finishes the work, finish the cleanup too.**

The task is done, but temporary files are scattered around, old drafts remain, and names, paths, and references in the documentation no longer match the result.

Coda helps AI close out the work: organize deliverables, correct confirmed errors, and clear obsolete temporary artifacts. Close out one task or review an entire workspace; proposed historical changes are listed for your approval before those items are changed.

[Quick start](#quick-start) · [Choose a scope](#choose-a-scope) · [Install and invoke](#install-and-invoke) · [Boundaries](#boundaries) · [简体中文](README.md)

## When to use Coda

| What you asked AI to do | What to check at closeout |
| --- | --- |
| Write reports, edit documents, or prepare a handoff | Find the final version, correct evidenced wording and naming errors, and align indexes and references with the actual deliverables |
| Research, process data, or create images and other content | Align sources and deliverable entry points, identify obsolete intermediate artifacts, and retain originals and required dependencies |
| Write code, debug, or run tools | Align documentation and paths, check whether temporary files are still needed, and review task-owned temporary processes |

Two independent, instruction-only skills. Sources are in English; responses follow your language. The skills themselves need no scripts, runtime dependencies, or network services. Task-specific tools and permissions come from the client. Run only when explicitly requested.

## Quick start

### Copy this prompt and ask AI to install

Send this to an AI client that supports skill installation and has permission to perform it:

```text
Install both the coda and coda-workspace skills from this repository:
https://github.com/H-Bole/coda
```

The installing AI should first read [Install and invoke](#install-and-invoke), identify both skill directories, the host, and any existing installation manager, and avoid duplicate entries or overwriting existing settings. After installation, refresh skills or start a new session and check that both entries are discoverable.

### First use in Codex

Close out the current task:

```text
$coda Close out the current task.
```

Review the whole workspace:

```text
$coda-workspace Review this workspace and list historical candidates for organization, correction, and cleanup.
```

You can also choose the entry in the skill picker. See [Claude Code](#claude-code) below for its invocation and configuration.

## Choose a scope

| Skill | When to use it | Historical material |
| --- | --- | --- |
| [`coda`](skills/coda) | Finish the current task: organize deliverables, correct confirmed errors, and clear obsolete artifacts and temporary processes | Leave unrelated historical material alone |
| [`coda-workspace`](skills/coda-workspace) | Close out a workspace: review organization, correction, and cleanup candidates | List specific historical corrections, moves, removals, and shutdowns; obtain approval for each, then recheck and skip changed items |

Each skill contains a complete `SKILL.md` and `agents/openai.yaml` and can be installed independently. Neither triggers automatically when work finishes or requires a new summary file after each task.

### A document closeout example

AI has just completed a report. Task records identify the final deliverable as “Research report,” but the handoff says “Reserach report” and links to a missing draft, while the final file already exists.

Coda should use the actual deliverable to correct the name and entry point, retain source material and referenced attachments, and remove a draft only after establishing that it belongs to this task, is obsolete, and is neither referenced nor in use. Keep old files of unknown ownership.

This is an illustrative workflow. Report issues and suggestions when meaning, facts, or choices remain uncertain. Historical corrections use the workspace skill's approval procedure.

## Why I made Coda

After a stretch of intensive Vibe Coding, I kept finding that Codex finished the job and left a mess behind. Ask it to clean up, and it would say the operation was blocked. I was still the one left cleaning up after it.

In that particular case, a batch cleanup was blocked, but checking and deleting items individually worked. I put that experience into Coda, along with deliverable organization, wording and reference corrections, and workspace-wide closeout.

Writing documents, researching, and creating content leave loose ends too. Coda is for any AI task that needs a proper closeout.

That success came from narrowing an already authorized operation and rechecking each item. An explicit prohibition or another block on the narrower operation still means stopping and reporting the limitation.

## Install and invoke

### Instructions for the installing AI

1. Read this repository's documentation and identify [skills/coda](skills/coda) and [skills/coda-workspace](skills/coda-workspace) separately. The repository root is not a single skill directory.
2. Check the host's supported skill locations, existing same-named skills, and installation management. Preserve existing settings and shared sources; do not migrate working installations merely because another client uses a different location.
3. Install both complete skill directories using the host or existing manager's supported method. For an existing same-named entry, check its source and version; confirm the user's update intent before replacing an installation. Preserve unrelated skills and avoid duplicate entries.
4. Configure explicit invocation as described below. Refresh skills or start a new session, check that each entry appears once, and report the installation locations and any remaining user steps.

This repository supplies skill files, without an installer script. Installation does not grant additional permission to change system settings.

### Manage with Magpie

1. Obtain the [repository](https://github.com/H-Bole/coda) using an import method supported by your Magpie installation.
2. Import both skill directories separately: [skills/coda](https://github.com/H-Bole/coda/tree/main/skills/coda) and [skills/coda-workspace](https://github.com/H-Bole/coda/tree/main/skills/coda-workspace). Do not assume importing the repository root installs both.
3. Refresh the host or start a new session and confirm that each skill appears once.
4. Manage updates and uninstallation through Magpie, retaining sources that other installations may share. Do not manually add links duplicating the existing manager's installation.

Magpie and the client determine the installation locations. Investigate installation or discovery failures before changing them. These instructions do not assume particular Magpie menu names.

### Codex

Choose a skill in the skill picker or explicitly enter `$coda` / `$coda-workspace`. CLI and IDE hosts supporting `/skills` can also use that entry point. `/coda` is not guaranteed to be a Codex slash command.

Both `agents/openai.yaml` files declare `policy.allow_implicit_invocation: false` so that the skills are used only when explicitly invoked.

### Claude Code

Invoke `/coda` or `/coda-workspace`. Both skills use standard, portable frontmatter. See below for host-level explicit-invocation settings. Claude Code has not been tested in a live installation.

<details>
<summary>Claude Code: configure user-only invocation</summary>

Merge this into your existing host settings structure, preserving other settings:

```json
{
  "skillOverrides": {
    "coda": "user-invocable-only",
    "coda-workspace": "user-invocable-only"
  }
}
```

This setting applies to personal or project directory skills, not plugin-provided skills. The user or installation manager handles host settings. Skill-body instructions alone cannot prevent implicit invocation at the host level.

</details>

See the [Codex skills documentation](https://learn.chatgpt.com/docs/build-skills) and [Claude Code skills documentation](https://code.claude.com/docs/en/skills) for invocation and configuration.

## Boundaries

- **Check before acting.** Read project rules and establish ownership, references, dependencies, and current use. Names, timestamps, and Git status alone do not prove something is disposable.
- **Corrections need evidence.** Use task requirements, actual deliverables, and trustworthy sources to correct clear in-scope errors while preserving meaning and structure. Report uncertain meanings or facts with suggestions; an inaccessible reference alone does not prove it is wrong.
- **Approve historical changes first.** List specific objects, evidence, and actions for historical corrections, moves, removals, and shutdowns. Recheck before acting; skip changed content, references, use, or identity and obtain fresh approval.
- **Keep what is needed.** Preserve originals, final deliverables, necessary dependencies, shared resources, and anything active or of unknown ownership. Leave reasonable output locations in place; check references and conflicts before a necessary move.
- **Match process identity.** Use task association, start time, and command line, and recheck before shutdown. PID, name, or port alone is insufficient. Preserve unrelated, persistent, shared, or uncertain processes.
- **Handle Windows items individually.** Prefer exact absolute paths with `Remove-Item -LiteralPath`, without `-Force` or `-Recurse` by default. Inspect directory contents, handle justified entries, then remove empty directories. Check links and parent path boundaries; remove only the link without entering shared targets.
- **Narrow a blocked batch when authorized.** An already authorized cleanup may use the same tool with one deletion command and one exact path per invocation, rechecking each item without force or recursion. Historical actions still need specific approval. Stop on an explicit prohibition or another block; report the limitation without switching tools or escalating privileges. `blocked by policy` alone does not establish an automatic approval rejection.
- **Keep closeout bounded.** Do not turn it into wholesale polishing, business changes, or an unsolicited audit. Do not clear shared caches, install dependencies, broaden tests, commit, or push by default.

Briefly report what was organized, corrected, deleted, stopped, retained, or skipped, plus unfinished or unverified work. Keep logical file size separate from actual disk-space changes; do not claim reclaimed space without measurement.

## Validation status

Validation covers skill format and entry configuration checks, plus correction and cleanup checks in isolated scenarios. Scenario walkthroughs are not independent model evaluations or host acceptance tests.

Installation, refresh, and invocation require acceptance checks in the target client. Neither the one-prompt AI installation nor Magpie installation has been tested end to end for this document; Claude Code has not been tested in a live installation. Visible entries alone do not verify every behavioral boundary.

Share real-world problems through [Issues](https://github.com/H-Bole/coda/issues). If Coda helps, a Star is welcome too.

[Glossary](GLOSSARY.md) · [MIT license](LICENSE)
