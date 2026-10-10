# Earlier error, timeout, and workflow solutions

These procedures preserve the earlier mass-apply solutions. Follow the current user's saved authorization, preferences, and active tool rules. Keep application-specific data in the separate private workspace.

| Problem | Saved solution | Verification or checkpoint |
|---|---|---|
| Employer portal reports Internal Error, including resume upload errors | Wait at least 60 seconds before refreshing, using the saved recovery preference. Inspect fresh page state afterward. | Recheck the same requisition, actual attachment, answers, and whether a submission occurred. Waiting alone does not prove recovery. |
| Submit produces no response or the browser times out | Record `submission_unknown`, then inspect employer confirmation, application history, or an existing-application notice. Refresh the same application when appropriate. | Retry Submit at most once only when evidence establishes that no submission occurred. A reappearing form alone does not establish this. Otherwise preserve the unknown outcome and continue other jobs. |
| Applications are submitted too close together | Keep submissions at least 120 seconds apart under the saved pacing preference. | Use the prior submission-attempt time, including uncertain attempts. Never invent a confirmation to satisfy pacing. |
| Jobright's resume modal detaches browser control | Save the entered answers and submission-attempt state. Before submission, a normal employer-page reload or fresh tab can restore control. | Refill from verified records and inspect the actual employer form. Reconcile an attempted submission before further action. |
| Jobright selects a resume but the employer form has no attachment | Choose the approved role-specific saved resume and Original Version. Use the supported native employer file chooser if needed. | Verify the actual attachment filename and the approved source PDF's hash; a selected Jobright name is insufficient. |
| PDF upload is unavailable | Use the employer's native Enter manually resume option when supported, with exact text extracted from the approved PDF. | Preserve dates and content, save the submitted text and PDF hash, and record `resume_delivery=employer_resume_text`. If a file is mandatory, checkpoint the role and continue. |
| Autofill is unavailable or contains stale answers | Compare the extension profile with current verified local facts. Fill missing fields manually using supported controls. | Stop unsafe autofill until incorrect sensitive values are corrected. Check complete dates, autocomplete selections, and toggles after page reflow. |
| A tab, login, or saved session expires | Reopen the checkpoint URL, verify the same live requisition and intended account, then sign in through the authorized flow. | Resolve any possible submission first; refill from verified saved answers and resume sources. A saved tab is not durable evidence of a live session. |
| CAPTCHA, non-email MFA, missing required facts, or a required user confirmation blocks one role | Save a resumable checkpoint and leave the page available when supported. Continue other eligible jobs. | Record application identity, URL, last step, verified non-secret answers, resume/hash, blocker, next action, evidence, and `submission_attempted`. Never bypass the challenge or save authentication secrets. |
| Employer email sign-in or account activation is required | Within saved authorization, retrieve only the matching recent message for the same account and employer/ATS flow. | Match recipient, sender/domain, portal, and challenge time. Keep codes and tokenized activation links transient. This does not enable background Gmail status sync. |
| A role may already have been applied to | Match employer, ATS tenant, and exact requisition against canonical records and employer history. | Different requisitions remain separate; similar titles are only a warning. Never blindly reset blocked, applied, or unknown records. |
| One application fails during a batch | Immediately save its precise status, blocker, next action, and evidence; append an event, read the row back, and continue. | Use `submission_unknown` for failures at or after a submit attempt. Stop the batch for a shared account mismatch, unsafe autofill, or duplicate-submission risk. |
| Excel export fails or a workbook is stale | Preserve canonical CSV/events, record export pending, and retry the workbook export separately. | Preserve user-added sheets and all fields. Verify application ID, status, resume delivery, and confirmation after export. Never resubmit because Excel failed. |
| Skipped jobs clutter the Excel view | Exclude skipped rows from the displayed Applications sheet according to saved preferences. | Retain skipped records and events in canonical history for duplicate prevention. Preserve the Email Log and unrelated workbook content. |
| Tracking updates may overwrite newer records | Re-read by stable application ID and requisition; use a single writer, temporary-file validation, and atomic CSV replacement. | Preserve existing fields, evidence, user edits, and destination-only records. Reconcile conflicting updates before replacing anything. |
| A scheduled run risks sleep or exceeds its limit | Use the available native OS sleep inhibitor for the remaining authorized duration, bounded by the configured hard stop. | Save source cursors, counters, active application state, and summary before stopping. Do not use site keepalive loops, auto-clickers, or auto-refreshers. |
| A connector operation times out | Inspect the destination state before retrying a write. Use another authorized connector only when the operation's state is resolved. | Never replay the same uncertain write through multiple connectors. Verify the intended connected account and actual operation support. |
| Repeated prompts ask for facts or approval already supplied | Reuse confirmed answers with matching question meaning and scope, and apply existing destination/data consent. | Unknown facts remain unknown. Ask only for missing required facts or a concrete exceptional confirmation required by active tools. |

## Submission evidence

Immediately before the final click, persist `submission_attempted` and `submission_unknown`. Mark `applied` only after an employer success message, receipt, or application-history entry verifies the outcome. Jobright badges, button clicks, disappearing forms, and URL changes alone are insufficient. Clear employer success with failed screenshot storage is still a submission; record the evidence limitation and do not submit again.

## Supporting instructions

- [Full workflow and recovery](SKILL.md)
- [Resume delivery, detached browser control, and expired sessions](references/jobright.md)
- [Application identity, status meanings, checkpoints, and Excel](references/records.md)
- [Connector selection and verification codes](references/composio.md)
- [Optional Gmail reconciliation](references/gmail-sync.md)
- [Discovery and duplicate prevention](references/discovery.md)

## Scope of preservation

The public branch saves reusable procedures and their earlier timing choices. Personal answers, application evidence, trackers, resumes, credentials, and sync snapshots stay outside this branch. The original local workspace and its installed skill remain unchanged.
