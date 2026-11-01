# Coda Cleanup

The language used to describe cleanup scope and the status of artifacts left by a task.

## Language

**Current task (本轮)**:
The work covered by the user's active request, including explicitly accepted follow-up work. It excludes unrelated earlier work in the same workspace.
_Avoid_: Current session, everything recent

**Workspace cleanup (工作区收尾)**:
A review of the workspace for organization and cleanup, including historical leftovers. Its scope can extend beyond the current task.
_Avoid_: Full purge, automatic cleanup

**Historical leftover (历史遗留)**:
An artifact or process from work outside the current task that remains in the workspace. Its continued presence does not establish that it is obsolete.
_Avoid_: Old junk, stale file

**Cleanup candidate (清理候选)**:
A specific artifact or process proposed for removal or shutdown, pending a decision about whether it is safe and authorized. Candidate status is not approval.
_Avoid_: Disposable item, deletion target

**Final deliverable (正式成果)**:
An artifact intended as an enduring result of the work, including an output accepted by the user. It is distinct from temporary material used to produce it.
_Avoid_: Temporary output, leftover
