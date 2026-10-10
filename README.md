# Reusable job application solutions

This branch preserves the reusable `apply-to-job` skill and the error, timeout, upload, duplicate-prevention, and tracker solutions developed in the mass-apply workspace through October 9, 2026.

Start with [RECOVERY.md](RECOVERY.md) for the collected solutions, then [SKILL.md](SKILL.md) for the full application workflow. Supporting instructions are in [references/](references/).

This branch has independent Git history and contains only reusable documentation and skill metadata. Personal profiles, answers, resumes, application records, browser state, workspace snapshots, and machine schedules are excluded. It does not change the repository's existing main branch or its earlier history.

## Use the skill

Copy `SKILL.md`, `agents/`, and `references/` into your own `apply-to-job` skill directory. Set up your separate application workspace and its private records before running applications. Reuse current saved preferences and authorization; do not treat this guide as permission to submit applications or disclose data.

The recorded 60-second portal recovery delay and 120-second submission interval are the earlier workspace's timing choices. Configure those values in your own private preferences and honor later user changes. A delay is not proof that an error recovered.

The copied skill supports multiple discovery and tracking modes. Current workspace instructions and preferences determine which sources are allowed and whether Gmail status sync is enabled. Disabled status sync stays disabled; narrowly authorized sign-in or activation reads are separate operations.

## Source and verification

Reusable skill files were copied from local commit `214f332` without importing its Git history. The recovery guide summarizes saved workspace instructions and verified workflow records. Publication checks verify the file allowlist, unchanged source files, Markdown links, and independent commit history. They do not rerun employer applications or establish that a live portal is currently working.
