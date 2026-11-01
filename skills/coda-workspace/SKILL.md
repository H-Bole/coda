---
name: coda-workspace
description: Close out a workspace when the user explicitly requests workspace-wide organization and cleanup. Present historical cleanup candidates for specific approval before acting. Do not use for automatic task completion or a current-task-only wrap-up.
---

# Coda — workspace closeout

Run only when explicitly invoked or when the user expressly asks for workspace closeout. Finishing another task is not a trigger. Reply in the user's language. Work within existing permissions and applicable project rules; invoking this skill does not authorize unrelated operations or historical deletion by itself.

## Establish scope and candidates

- Read applicable project instructions. Establish the workspace boundary, current task, formal deliverables, and continuing work from the conversation and available records. Do not invent missing history or expand to unrelated projects or user storage.
- Distinguish proven current-task artifacts from historical or uncertain items. Before proposing any cleanup, check ownership, references, dependencies, and current use. A filename, timestamp, untracked status, or ignore rule cannot independently establish that something is disposable. Retain resources with unresolved ownership or use rather than presenting guesses as safe candidates.
- Current-task artifacts may be cleaned only when their creation for this task and obsolescence are established. Historical resources include files, directories, or processes originating before the current task; their cleanup requires the approval procedure below.
- Present a bounded historical candidate list in the conversation: exact path or process identity, proposed action, evidence of obsolescence, and relevant reference/use checks. A directory candidate must describe its checked contents, not authorize unknown descendants. Do not create a permanent inventory file by default.
- Wait for the user's approval of specific candidates. A general request to clean the workspace is not approval of historical candidates. While approval is pending, safe organization and independently justified current-task cleanup may continue. Do not remove, move, or terminate historical candidates before approval.
- Immediately before executing an approved action, recheck the same object's identity, relevant content, references, and use against what was presented. Skip changed, replaced, newly referenced, or newly occupied candidates; report why and require fresh approval of a revised candidate before acting. Never transfer approval to a new object at the same path or PID.

## Organize and execute

- Preserve originals, formal deliverables, necessary dependencies, and anything referenced or still in use. Retain unknown or shared resources. Keep reasonable existing output locations; check references and destination conflicts before a necessary move, and never overwrite or break references. Historical moves use the same candidate approval procedure.
- Update existing documentation or entry points only where useful to locate or use results. Do not create a summary document for every run.
- Recheck each object immediately before mutation, including current-task items. Inspect a directory's remaining contents and handle only individually justified entries; an approved directory does not cover subsequently added contents.
- Resolve exact absolute operation paths and inspect link/reparse-point boundaries, including parent components. A link inside the workspace is not permission to traverse or clean external/shared targets. Limit external temporary cleanup to exact artifacts whose creation for the current task is established.
- On Windows, prefer `Remove-Item -LiteralPath` with an exact absolute path, without `-Force` or `-Recurse`. Handle justified entries individually, then remove an inspected empty directory. For junctions and symbolic links, verify type and target and remove only the link itself without following the target. If safe link-only removal is unavailable, retain it.
- Close only proven task-related temporary processes no longer needed; historical ones also require candidate approval. Match creation/start time, command line, and task records, not just PID, name, or port. Recheck identity before a graceful shutdown and verify the outcome. Retain shared, persistent, active, or uncertain processes; do not force-kill them or sweep a process tree.
- On failure or a policy block, stop that operation and report the limitation. Do not switch tools to bypass the block. Continue independent safe operations.

Do not default to clearing shared caches, installing dependencies, changing business code, broad testing, creating permanent tests, committing, pushing, or publishing. This closeout request grants none of those additional permissions. Do not create a cleanup engine or recurring automation.

## Report and finish

Briefly report useful organization, successful deletions, closed processes, pending historical candidates, retained/skipped items with reasons, and unverified operations. Omit empty categories. Distinguish the logical size of successfully deleted files from measured disk space actually freed; do not equate them or count failed deletions or link targets. If nothing needed doing, say so and finish normally. Repeated invocation must not create new work, duplicate inventories, or treat a previous approval as permission for changed resources.
