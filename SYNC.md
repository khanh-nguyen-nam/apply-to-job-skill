# Syncing this skill between Mac and Linux

This directory is the Git working copy installed as the `apply-to-job` Codex skill on both machines. The repository contains the skill only; applicant data belongs in the separate `mass-apply/private/` workspace and must never be added here.

GitHub receives changes after you commit and push them. Before editing on either machine, pull first; after editing, commit and push; on the other machine, pull to receive the update.

```sh
cd ~/.codex/skills/apply-to-job
git pull --ff-only
# edit the skill
git add -A
git commit -m "Update apply-to-job skill"
git push
```
