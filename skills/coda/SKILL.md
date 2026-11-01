---
name: coda
description: Close out the current task when the user explicitly requests a wrap-up. Organize deliverables and remove only proven obsolete artifacts and temporary processes from this task. Do not use for automatic task completion or historical workspace cleanup.
---

# Coda — current-task closeout

Run only when explicitly invoked or when the user expressly asks for closeout. Finishing another task is not a trigger. Reply in the user's language. Work within existing permissions and applicable project rules; invoking this skill does not authorize unrelated operations.

## Establish scope

- Read applicable project instructions. Identify the current task, workspace boundary, deliverables, and any continuing work from the conversation and available records. Do not invent missing history.
- Limit cleanup to artifacts and processes demonstrably created for this task and now obsolete. Never broaden to historical workspace cleanup. Ask only if missing scope blocks an operation; otherwise retain uncertain items and continue safe work.
- Before acting, check ownership, references, dependencies, and current use. A filename, timestamp, untracked status, or ignore rule is not sufficient evidence of ownership or disposability. Session creation records and an artifact's demonstrated purpose can establish ownership; ownership alone does not establish obsolescence.

## Organize and clean

- Keep originals, formal deliverables, necessary dependencies, and anything referenced or still in use. Retain unknown or shared resources. Preserve reasonable existing output locations. Before a necessary move, check references and destination conflicts; do not overwrite or break references.
- Update existing documentation or entry points only where useful to locate or use the result. Do not manufacture a new summary document for every closeout.
- Remove only proven obsolete task artifacts. Immediately before each mutation, recheck the object's identity, relevant content, references, and use. If anything changed or cannot be verified sufficiently, skip it. Do not delete a directory based only on its name: inspect its remaining contents and handle only individually justified entries.
- Resolve the absolute operation path and inspect link/reparse-point boundaries, including parent components. Stay within the established workspace, except for exact external temporary artifacts whose creation for this task is established. Do not expand a targeted operation into a scan of external or shared storage.
- On Windows, prefer `Remove-Item -LiteralPath` with an exact absolute path, without `-Force` or `-Recurse`. Process justified directory entries individually, then remove an inspected empty directory. For a junction or symbolic link, verify type and target and remove only the link itself, without following it into the target. If safe link-only removal is unavailable, retain it.
- Close only temporary processes proven to belong to this task and no longer needed. Match creation/start time, command line, and task records; PID, process name, or port alone is insufficient. Recheck identity immediately before a graceful shutdown and verify the outcome. Retain shared, persistent, active, or uncertain processes; do not escalate to force-killing them or sweeping a process tree.
- Stop a failed operation before deciding the next step. If a batched cleanup command is blocked and cleanup is already authorized, a narrower attempt may use the same tool with exactly one literal absolute path and one deletion command per tool invocation, without force or recursion. Recheck each object, and inspect directories before removing them empty. This does not permit overriding an explicit prohibition, changing tools, or escalating privileges; if the narrower attempt is also blocked, stop and report the exact leftovers and limitation. A `blocked by policy` message alone does not establish an automatic approval rejection. Continue independent safe operations.

Do not default to clearing shared caches, installing dependencies, changing business code, broad testing, creating permanent tests, committing, pushing, or publishing. This closeout request grants none of those additional permissions. Do not create a cleanup engine or recurring automation.

## Report and finish

Give a short account of useful organization, successful deletions, closed processes, retained/skipped items with reasons, and unverified operations. Omit empty categories. Distinguish the logical size of successfully deleted files from measured disk space actually freed; do not equate them or count failed deletions or link targets. If nothing needed doing, say so and finish normally. Repeated invocation should not create new work or extra artifacts.
