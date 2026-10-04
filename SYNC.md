# Syncing this skill between Mac and Linux

This directory is the Git working copy installed as the `apply-to-job` Codex skill on both machines. On October 4, 2026, the user authorized a filtered personal workspace snapshot in this existing private repository for Mac synchronization. See `sync/README.md`. Keep applicant data out of distributable skill packages; the snapshot is for this user's private cross-machine sync only. Never upload authentication secrets or browser sessions.

GitHub does not mirror unsaved edits. Changes sync after you commit and push them; pull on the other machine to receive them. On Linux, authenticate the private-repository checkout once with GitHub CLI: `gh auth login --hostname github.com --git-protocol https`, then run `gh auth setup-git`. Before editing on either machine, pull first; after editing, commit and push; on the other machine, pull to receive the update.

```sh
cd ~/.codex/skills/apply-to-job
git pull --ff-only
# edit the skill
git add -A
git commit -m "Update apply-to-job skill"
git push
```

## Files outside Git

The authorized `sync/workspace.tar.gz` snapshot now transports the separate application workspace through this private GitHub repository. SCP remains an optional alternative. Never copy the snapshot into a distributable skill archive. Verify its manifest and SHA-256, stage it, and reconcile destination-only/newer changes before installing it.

Work on one machine at a time. Before switching machines, save the workspace and copy it over SSH with `scp`; verify file hashes before resuming. If both machines have changes, take snapshots of both and reconcile them first. Never overwrite a confirmed submission or replace a newer tracker with an older copy. SCP copies files; it does not merge changes or delete destination-only files.

Copy into a staging directory before installing the reconciled files. Preserve destination-only artifacts and keep backups. Resolve configured paths relative to the workspace (for example, `private/resumes/resume.pdf`) so records work on both platforms. Retain machine-specific browser/session and scheduler settings when applicable.

Do not copy Git's `.git/` directory, browser profiles, authentication tokens, SSH keys, password-manager databases, dependency caches or `node_modules` links. GitHub authentication stays local to each machine. Exclude sync backups and active lock files from subsequent workspace transfers; set private files to owner-only permissions.

The workspace's `SYNC-PRIVATE.md` records its SSH destination, file-transfer procedure, and backup location. Reusable skill changes follow the Git workflow above; workspace changes follow that SCP workflow.
