# UW Residence Response — Product Plan

## Vision

Give residence students a fast, clear, and reliable way to reach the correct University or emergency support service without searching for phone numbers or remembering complex responsibilities and operating hours.

## Problem

Residence students receive several important contact numbers during their first community meeting, including Duty Don, front desk, Special Constable Service, Campus Response Team, and 911. Many students do not save the numbers or do not remember which service handles which situation. This creates confusion, delays, and calls that must be forwarded.

## Users

### Primary user

A University of Waterloo student currently living in Campus Housing, particularly a new resident who is unfamiliar with campus services.

### Administrative user

An authorized Campus Housing staff member who maintains residence-specific phone numbers, service hours, term dates, and temporary notices.

### Potential future user

A Duty Don or other responder who receives a consent-based alert associated with an initiated call.

## Product principles

1. Emergency access comes first; the app must never obstruct or delay 911.
2. A stressed student should understand the home screen within seconds.
3. Routing information must be approved, current, and auditable.
4. The app should collect the minimum personal data necessary.
5. A registered residence must not be treated as the student's live location.
6. Critical contacts must remain available during weak connectivity or login failure.

## MVP scope

### Student application

- Sign in through a prototype authentication flow; Waterloo SSO requires institutional approval and integration.
- Register residence, building/area, term, move-in date, and move-out date.
- Store a verified callback number.
- Display large, accessible contact actions for 911, Special Constable Service, CRT, Duty Don, and front desk.
- Filter Duty Don numbers by residence area, term, and effective date.
- Display current availability based on approved operating hours.
- Launch the native phone dialler only after showing the selected service and number.
- Provide a short “Not sure who to call?” guided decision flow.
- Display the registered residence address and warn the student to confirm their actual location.
- Cache approved critical contacts for offline use.
- Provide guest access to universal emergency contacts if authentication fails.

### Admin portal

- Role-based administrator access.
- Create and edit residences, residence areas, services, phone numbers, operating hours, and effective dates.
- Schedule future term configurations.
- Publish urgent temporary contact changes.
- Keep an audit history of changes.
- Preview what a student in a selected residence would currently see.

## Out of scope for MVP

- Replacing 911 or professional emergency dispatch
- Diagnosing medical conditions
- Automatically sending student IDs through SMS
- Assuming registered residence equals current physical location
- Recording calls
- Storing detailed incident narratives
- Production Waterloo SSO without University authorization
- Automatically exposing student information to an ordinary receiving cellphone

## Routing model

The routing engine should evaluate:

1. Whether the situation indicates immediate danger or a serious medical emergency
2. The selected service category
3. The student's residence area
4. Current date and academic term
5. Current time and approved service hours
6. Whether an active contact record exists
7. The safest fallback when data is missing or expired

If no valid residence-specific record exists, the app should show the universal emergency option and clearly report that the local contact is unavailable. It must never silently display an expired number.

## Student experience

### Onboarding

1. Open the app and review the emergency disclaimer.
2. Sign in or continue in guest emergency mode.
3. Confirm name and callback number.
4. Select residence and residence area.
5. Confirm term and residence dates.
6. Review privacy and location-sharing choices.

### Getting help

1. Open the home screen.
2. Select a clearly labelled service or “Not sure who to call?”
3. Review one short confirmation screen.
4. Start the native call.
5. Optionally share current location through a separate, explicit consent action in a future version.

## Data model

| Entity | Key information |
| --- | --- |
| User profile | Internal user ID, display name, verified phone number |
| Residence stay | User, residence area, start date, end date |
| Residence | Name, area, civic address, emergency entrance notes |
| Service | Name, purpose, urgency level, universal/residence-specific flag |
| Contact assignment | Service, residence area, phone number, effective start/end |
| Operating schedule | Service, timezone, day, opening time, closing time, exceptions |
| Admin account | User, role, permitted residence areas |
| Audit event | Actor, action, target record, timestamp, before/after summary |

## Privacy and security requirements

- Collect only necessary student data.
- Encrypt data in transit and at rest.
- Never store secrets in the mobile application or repository.
- Require explicit consent before sharing live location.
- Do not send student IDs or sensitive details by ordinary SMS.
- Apply least-privilege access to administrators.
- Log administrative changes and sensitive record access.
- Define retention and deletion rules before any real-user pilot.
- Complete a University privacy and security review before production use.

## Accessibility requirements

- Large touch targets and readable type
- Screen-reader labels for every action
- High-contrast design that does not rely only on colour
- Plain-language descriptions
- Minimal typing during urgent use
- Support for dynamic text sizing
- Logical keyboard navigation in the admin portal

## Delivery phases

### Phase 0 — Discovery and validation

- Interview students, Dons, Residence Life staff, front desk staff, SCS, and CRT.
- Confirm official responsibilities, hours, and escalation rules.
- Map current call-forwarding problems.
- Review privacy, legal, branding, and accessibility constraints.

### Phase 1 — Clickable prototype

- Design onboarding, home, contact confirmation, guided routing, and admin screens.
- Test comprehension with students using fictional numbers and scenarios.

### Phase 2 — Technical prototype

- Build the React Native app and admin portal.
- Use fictional residences, contacts, and users.
- Implement time-, term-, and residence-aware routing with tests.

### Phase 3 — Controlled pilot proposal

- Present evidence and prototype to Campus Housing and relevant safety teams.
- Incorporate official guidance.
- Complete security, privacy, and accessibility reviews.

### Phase 4 — Approved pilot

- Pilot in a limited residence area with monitored configuration ownership.
- Measure successful routing, usability, incorrect calls, and system reliability.

## Initial backlog

### Product and design

- Map services and responsibilities.
- Draft emergency decision-tree language.
- Create low-fidelity student screens.
- Create low-fidelity admin screens.
- Run five student usability sessions.

### Engineering

- Initialize the TypeScript monorepo.
- Define shared routing types and validation.
- Implement a deterministic routing engine.
- Add routing unit tests for time, term, residence, and missing-data cases.
- Build residence onboarding.
- Build the contact home screen.
- Build admin contact scheduling.
- Implement offline contact caching.

### Governance

- Identify the owner for every contact record.
- Define update and emergency-correction procedures.
- Draft privacy notice and consent language.
- Create a production-readiness checklist.

## Success measures

- Students select the correct service in scenario tests.
- Median time from opening the app to initiating the correct call.
- Reduction in calls forwarded to another service.
- Percentage of contact records with a named owner and future effective dates.
- Accessibility and usability test completion rates.
- Zero expired numbers silently shown as current.

## Major risks and mitigations

| Risk | Mitigation |
| --- | --- |
| Incorrect or expired number | Effective dates, ownership, audit history, preview, and safe fallback |
| App delays urgent care | Permanent 911 access and minimal confirmation steps |
| Service hours change | Admin schedules, exception dates, and cached configuration expiry |
| Privacy over-collection | Data minimization, consent, retention limits, and institutional review |
| Student is away from residence | Clear location confirmation and optional live location only |
| Network or authentication failure | Offline cache and guest emergency mode |
| Users treat guidance as diagnosis | Approved plain-language routing and no medical diagnosis |

## Future features

- Consent-based responder notifications matched to an initiated call
- Optional live location sharing
- Push alerts when residence contacts change
- Multilingual safety guidance
- Silent or text-based help options approved by safety stakeholders
- Anonymous aggregate analytics
- Integration with an approved campus telephony or dispatch platform

