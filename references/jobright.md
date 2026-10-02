# Jobright browser connection

Official workflow checked on 2026-10-01: [Jobright Autofill](https://jobright.ai/job-autofill) describes installing its extension, setting up a profile, opening an application, and using Autofill before submission. Recheck the live interface when it changes. No working Jobright connector was returned by this installation's plugin search; this is not evidence that none exists anywhere.

The authenticated Profile page's setup dialog additionally instructs opening the extension while on a Jobright page and choosing **Start Applying** to activate it. This activation step must be distinguished from starting a live application or enabling the separate Jobright Agent service.

## Setup and verification

1. Read `private/jobright.json`. Its connection state is a last observation, not proof that today's session still works.
2. Reuse the user's connected Chrome profile with the intended Jobright account. Inspect `https://jobright.ai/jobs/profile` and `https://jobright.ai/jobs/resume` through the visible UI. If login is required, use the normal authorized sign-in flow or hand off; never export authentication state into this project.
3. Obtain the extension listing from Jobright's live **Install Extension** control. The observed official listing is [Jobright Autofill](https://chromewebstore.google.com/detail/odcnpipkhjegpefkfplmedhmkmmhmoko), publisher website `jobright.ai`. Do not install a similarly named third-party extension. If browser DOM automation cannot access the Web Store or toolbar, use the supported native Chrome UI through the same computer-use tool.
4. Inspect the installation dialog's actual permissions. Follow the active tool's requirements for granting new access; do not claim installation from merely opening the listing. Verify the installed state in Chrome and record the result.
5. Open the extension while on Jobright. Verify the account matches, then complete the documented activation using the current UI. Do not silently enable paid features or autonomous discovery/submission services.
6. Import only confirmed local profile fields and the approved resume within the user's upload/data-sharing authorization. Preserve old resume variants until the user requests cleanup. Check parsed contact details, dates, work history, skills, work authorization, and sponsorship before using autofill. A site's “profile complete” indicator does not establish accuracy.
7. When the user supplies a target application, perform a preparation-only verification if requested, or the authorized application itself. Check autofilled values and the resume filename on the employer form. Record `autofill_verified_at` only after observing that it worked. Installation alone is not an end-to-end test.

## During application runs

- Prefer one active application at a time; extension/profile state can be shared across tabs. Avoid concurrent writers to the tracker.
- Follow **Apply with Autofill** or the extension's current visible action to the actual employer form. Inspect the destination before sharing data. Do not mistake a redirect or an extension recommendation for a submission.
- When autofill cannot operate, complete the form with confirmed local answers using supported controls. If file upload is needed, read the computer-use tool's current upload documentation; do not copy old sandbox-staging assumptions or rely on unverified APIs.
- Use signed-in Workday employer accounts when available. Record the exact employer login URL in the credential index because separate tenants can require separate accounts.
- Store Jobright display status separately from employer-confirmed submission status. Local files are the tracker for this setup. Never claim Jobright or a Google Sheet was synchronized unless its actual UI/API result was verified.
- If the installed extension sends incorrect sensitive answers, stop invoking it until those values are corrected or cleared. Manual correction afterward cannot undo an earlier disclosure.

## Verification and CAPTCHA

- When Jobright or an employer portal sends an email one-time code to the configured application mailbox during an authorized sign-in or account-creation flow, use the active Composio Gmail connection under [composio.md](composio.md). Search narrowly using the challenge time, sender/domain, and portal name; read only the matching message; enter the code into the same active browser flow; and do not store or display the code.
- Do not reuse an old code, guess when several messages match, or retrieve password-reset, account-recovery, security-alert, or unrelated-service codes. Record a handoff when the message or target is ambiguous, the mailbox differs, or verification requires SMS, authenticator, push approval, recovery data, or another person.
- A CAPTCHA is not an email verification code. Never send a CAPTCHA to Composio, use a Composio browser/proxy to avoid it, or switch sites/connectors to defeat it. Save `captcha_required`, preserve the page for the user, and continue the batch with other applications.
- Do not install or run an auto-clicker, auto-refresh extension, synthetic mouse/keyboard loop, or periodic keepalive request on Jobright or an employer site. These can alter form state, trigger unintended actions, and defeat site protections. A local scheduled run may use a native, bounded OS sleep inhibitor only to prevent the computer itself from sleeping; follow the OS-specific instructions in the skill entrypoint.
- At any user handoff, write `resume-checkpoint.json` in the application artifact with the URL, employer/ATS/requisition identity, captured time, last completed step, selected resume ID/hash, verified non-secret answers already used, blocker, next action, and `submission_attempted`. Preserve the tab when possible, but assume its session may expire. Never store passwords, cookies, one-time codes, CAPTCHA material, or recovery data.
- To resume an expired page, reopen the saved URL, verify the requisition and account, reconcile whether any submission occurred, and refill only from the checkpoint and current verified sources. Use the ATS's native save-and-return feature when available.

