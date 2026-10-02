# Local application records

All mutable user data is under `private/` in the configured workspace. Read only the portions needed for the task. Keep file permissions owner-only and keep this directory out of version control and exported skills. This is a local permission boundary, not encryption; browser sessions and password-manager items remain outside these files.

## Files

| File | Purpose |
|---|---|
| `profile.json` | Identity, education, work, skills, and links with provenance and confirmation state |
| `preferences.json` | Job filters, limits, automatic-submission preference, readiness |
| `answers.json` | Verified reusable answers, exact question meaning, and scope |
| `credentials.json` | One account entry per service/employer with sign-in method and password-manager reference; no secret values |
| `resumes.json` | Actual file paths, SHA-256 hashes, role mappings, and approval state |
| `jobright.json` | Observed connection, installation, profile-sync, and autofill-test state |
| `job-boards.json` / `discovery-state.json` | Board access status, worldwide search sources, coverage and continuation |
| `applications.csv` | One current record per employer requisition |
| `events.jsonl` | Append-only application changes and submission attempts |
| `authorization.md` | User's standing preferences and scope limits |
| `runs/` | Scope, filters, resume IDs, requested limit, authorization, and outcome summary per run |
| `applications/APP-ID/` | Posting, exact answers, selected resume hash, blockers, and confirmation evidence |
| `resumes/` | User-provided resume files; preserve original uploads |
| `sources/` | Read-only source observations; never automatically trusted as current |
| `gmail-sync.json` / `gmail-sync-state.json` | Gmail account, sync preferences, pagination, and completed checkpoints |
| `gmail-messages.jsonl` | Idempotent per-message classification and minimal evidence |
| `gmail-review.json` | Ambiguous receipts and updates awaiting reliable job matching |

For a browser handoff or expired session, store `applications/APP-ID/resume-checkpoint.json` with the application identity, exact URL, captured timestamp, last completed step, verified non-secret answers already used, selected resume ID/hash, blocker, next action, and whether submission was attempted. Do not store authentication secrets, one-time codes, cookies, CAPTCHA content/responses, passwords, or recovery data. Treat the checkpoint as refill input, not proof that the live page or session still exists.

## Confirmation and unknowns

In profile sections and answer entries, `confirmed: false` means the content needs confirmation or replacement. `null` means unknown, never “no.” A confirmed group means the user or approved current document supports its values; retain `source` and `confirmed_at`. An approved resume can support its work/education facts but cannot establish legal authorization, salary requirements, availability, or voluntary disclosure preferences.

The initial Jobright source snapshot is a stale reference, not an approved resume or a ready-to-submit answer bank. Confirming contact details does not approve all old work claims or demographics. A profile `confirmed_at` value is an ISO-8601 timestamp with timezone; update it from real confirmation, not setup time.

Add resume entries only for files that exist. Each entry needs `id`, `path`, `sha256`, `target_roles`, `approved`, `approved_at`, and `source`. Choose a default resume ID only after approval. Keep generated variants distinct from originals.

Reusable answer entries need `id`, `question`, `value`, `scope`, `confirmed`, `source`, and `confirmed_at`. Preserve the exact employer question and submitted response in the application artifact even when a reusable answer supplied it. Do not reuse a country-specific answer globally or treat two differently worded eligibility questions as equivalent.

## Job identity and tracker writes

Prefer employer + ATS tenant + requisition ID as the unique key. Preserve original URLs. For a fallback normalized URL, lowercase scheme/host, remove fragments and known marketing parameters such as `utm_*`, `gclid`, and `fbclid`. Preserve job-identifying query parameters, including `gh_jid`, `jobId`, and tenant identifiers. Resolve Jobright and employer URLs to the same row only with evidence of the same requisition. Similar company/title/location is a duplicate warning, not proof; distinct requisition IDs stay distinct.

Generate a stable local `application_id` once. Before any update, re-read and match both that ID and job identity. Use Python's `csv` module rather than manual comma splitting; escape commas/newlines correctly. Write the complete updated CSV to a temporary file in the same directory, read it back, then replace atomically, preserving owner-only permissions. Do not overwrite concurrent changes; use a single writer. Append an event with timestamp, application ID, prior/new status, reason, and evidence reference. If one write fails, stop mutations and reconcile from evidence on resume.

## Status meanings

| Status | Evidence / next action |
|---|---|
| `discovered` | Candidate recorded; not submitted or necessarily authorized |
| `queued` | Included in an authorized application run |
| `in_progress` | Form filling started |
| `prepared` | Form prepared; no final submission |
| `blocked` | Missing fact, login, required confirmation, or technical blocker; set `blocker` and `next_action` |
| `submission_unknown` | A submit may have occurred; reconcile before any further submit |
| `applied` | Employer confirmation, receipt, or account history verifies submission |
| `assessment`, `interview`, `offer`, `rejected`, `withdrawn` | Supported by employer communication, account state, or explicit user report |
| `skipped` | Confirmed filter mismatch or explicit exclusion, with reason |
| `closed` | Posting unavailable/closed, with evidence |

`applied_at` stays blank until confirmed and is preserved through later stages. Keep `jobright_status` as a separate observation. `resume_sha256`, `confirmation_url`, and `evidence_path` tie the row to actual artifacts. If a submit is confirmed but evidence-file storage fails, use `applied` and explain the limitation; do not resubmit to recreate proof. If no submit has been attempted and validation fails, use `blocked` or continue repair, not `applied`.

Never bulk-reset unresolved or submitted records to `queued`. Sorting is optional and must preserve complete rows. Empty CSV means no locally recorded applications, not proof that the user has never applied elsewhere; reconcile relevant history before a first live batch.

For Gmail, use [gmail-sync.md](gmail-sync.md). `submission_source` distinguishes bot, manual (only when known), and external_unknown. `status_updated_at` holds the event timestamp supporting the current status, not sync time. `last_email_at` can advance without changing status. `action_due_at` is populated only from an explicit deadline; otherwise leave blank. Preserve existing columns and data when adding fields.
