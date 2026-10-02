# Worldwide job discovery

Read `private/job-boards.json` for verified account access, public sources, and blockers. Read the current role, timing, country and work-rights preferences. Public web access is not an authenticated connector; report those states separately.

Use Jobright and LinkedIn browser sessions when signed into the user's verified account. Search public FirmwareJobs, Gradcracker, EURES, SEEK, Jobstreet and employer career pages using the available browser/search tools. Indeed currently requires the user's review of updated binding terms; do not retry unchanged blockers. Do not install employer-side recruiting plugins to search applicants' jobs.

## Coverage and efficient searching

- Search firmware/embedded/RTOS/BSP, Linux/kernel/drivers, and systems/platform/low-level software as separate families. Combine each with graduate/new-grad/junior/entry-level and intern/internship/co-op terms. Include relevant local-language title equivalents, without claiming the user speaks those languages.
- Search every region in preferences, rotating countries across runs rather than repeatedly searching only the U.S. or nearby cities. Remote positions still have employment-country restrictions. A board's default or home-location radius must not narrow worldwide scope silently.
- Honor `geography.excluded_countries` before adding candidates and again before preparing applications. Apply exclusions to employment location, not employer headquarters. For multi-country roles, verify an eligible destination.
- Read current source and location capabilities from the live UI; set each search location explicitly rather than trusting default recommendations. Record any UI limitation.
- Prefer compact search/list results. Reject obvious unrelated senior/lead/manager roles before fetching descriptions. Do not require Easy Apply or a sponsorship keyword: unknown sponsorship is a review item, not proof of either eligibility or ineligibility.
- Follow promising leads to the employer or ATS, verifying requisition, current availability, location, start date, seniority, and eligibility. Search snippets and stale repository lists are leads, not verified openings.
- Deduplicate against `applications.csv` by employer/tenant/requisition and canonical destination. Keep multiple discovery sources as notes on the same requisition, not multiple applications. Never overwrite an applied/interview/rejected record with discovered.
- Use bounded passes with a saved next source/region/page so later runs continue. Stop a source after two pages yield no new relevant leads. Save coverage in `private/discovery-state.json`; report new distinct leads and coverage gaps, not an unsupported count of every available job.

## Authorization and eligibility

Resolve country-specific work rights, enrollment, and start-date conditions from current verified private sources for each affected application. A work-authorization or sponsorship answer for one country does not establish eligibility in another.

Discovery can continue while application eligibility is unresolved. Record candidate leads as `discovered`, with specific review items. A new application batch or recurring search schedule must have its own scope; the existing 12-hour Gmail monitor does not itself run job discovery or submit applications.
