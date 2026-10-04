# Mac workspace sync

The user authorized this personal snapshot in the private `khanh-nguyen-nam/apply-to-job-skill` repository on October 4, 2026. Keep this repository private. The reusable skill remains at the repository root; never include `sync/` in a distributable skill package.

`workspace.tar.gz` contains the saved application workspace, including approved resumes, profile and answers, authorization, Jobright-only preferences, CSV/Excel trackers, email evidence/review, application checkpoints, run summaries, and supporting workspace files. `manifest.json` records SHA-256 hashes of every included file. Browser sessions, authentication secrets, active locks, dependency links, and recursive sync backups are excluded.

Current workflow: Jobright discovery and Apply with Autofill; local-sheet tracking after the final Gmail snapshot. Recurring Gmail status sync is paused. Narrow sign-in-code reads and matching account activation links after authorized employer signup remain authorized. Use the approved common email and an accessible saved common password; keep credentials and activation tokens out of GitHub. Linux application schedule uses GPT-6 Sol / Low; the paused Gmail schedule retains GPT-6 Luna / Medium.

## Pull and stage on Mac

```sh
cd ~/.codex/skills/apply-to-job
git pull --ff-only
shasum -a 256 -c sync/workspace.sha256
MAC_SYNC_STAGE=$(mktemp -d)
chmod 700 "$MAC_SYNC_STAGE"
tar -xzf sync/workspace.tar.gz -C "$MAC_SYNC_STAGE"
printf 'Staged workspace: %s\n' "$MAC_SYNC_STAGE"
```

Ask Codex on the Mac to reconcile that staged snapshot with `/Users/macboookpro/khanh-dev/mass-apply`, preserving destination-only evidence, newer outcomes, application IDs and user edits. Do not overwrite the live Mac workspace while either machine is applying or editing its tracker. Back up the Mac workspace first. Shared resume paths are relative; machine-specific absolute paths/browser IDs are observations to rediscover, not portable settings. Use Mac's current workspace path when running the workflow.

`linux-automations/` contains schedule exports for reference. Do not copy them into the Mac automation directory or enable duplicate schedules; Linux remains the execution host. Authenticate GitHub and Jobright separately on Mac. Keep installed private directories owner-only (700) and files owner-only (600).

The latest sheet is `private/applications.xlsx` within the snapshot. New emailed outcomes after the final snapshot are not automatically imported.
