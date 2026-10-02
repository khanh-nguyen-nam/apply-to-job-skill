# Syncing this skill between Mac and Linux

This directory is the Git working copy installed as the `apply-to-job` Codex skill on both machines. The repository contains the skill only; applicant data belongs in the separate `mass-apply/private/` workspace and must never be added here.

GitHub does not mirror unsaved edits. Changes sync after you commit and push them; pull on the other machine to receive them. On Linux, authenticate the private-repository checkout once with GitHub CLI: `gh auth login --hostname github.com --git-protocol https`, then run `gh auth setup-git`. Before editing on either machine, pull first; after editing, commit and push; on the other machine, pull to receive the update.

```sh
cd ~/.codex/skills/apply-to-job
git pull --ff-only
# edit the skill
git add -A
git commit -m "Update apply-to-job skill"
git push
```
