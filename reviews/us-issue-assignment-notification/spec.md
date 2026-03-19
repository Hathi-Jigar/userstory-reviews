# SECTION A — USER STORY / FEATURE PRD

---

**📝 User Story: Issue Assignment with Assignee & Notification Recipients**

**Module / Area:** Instructions (Issue Module)

**Type:** Enhancement

**Interactive Prototype:**
- [View Live Screen](https://digiqc-hq.github.io/product-management/screens/us-issue-assignment-notification/)
- [View Source Code](https://github.com/digiqc-hq/product-management/blob/main/docs/screens/us-issue-assignment-notification/index.html)

**Test Cases:**
- [Mobile & Web Admin Test Cases](https://github.com/digiqc-hq/product-management/blob/main/test-cases/US-issue-assignment-notification/US-issue-assignment-notification-testcases.md)

---

**📌 Brief Description**

When a field user raises an issue, they currently assign it to one person. This enhancement adds the ability to also select one or more people to be notified when key events happen on that issue — such as when it is raised, responded to, rejected, accepted, or closed. The assignee and the notified users each receive targeted notifications based on their role in the issue. This feature is controlled at the organisation level by the Super Admin and applies to all projects in that organisation when enabled.

---

**🎯 Jobs to Be Done (JTD)**

| Role | When… | They want to… | So they can… |
|------|--------|---------------|--------------|
| Site Engineer / QC Inspector | Raising an issue on-site | Assign it to one responsible person and optionally loop in other stakeholders | Ensure the right people know about the issue without having to chase them manually |
| Project Admin | Overseeing issue resolution | Make sure all relevant parties — across teams — are kept informed automatically | Track issue progress without manually broadcasting updates |
| Admin / Super Admin | Configuring the platform for their organisation | Turn on the notification feature once at the org level | Have it apply uniformly across all projects without project-by-project setup |
| Assignee (Team User) | Being assigned an issue | Receive a clear notification that they have been made responsible | Take action immediately without missing any assignment |
| Notified User | Being looped in on an issue | Get relevant updates without being the assignee | Stay informed on issues that affect their work or team |

---

**💡 How Might We (HMW)**

- How might we make it easy for a field user to pick the right person from potentially many project team members, without overwhelming them?
- How might we clearly distinguish between "who is responsible" and "who needs to stay informed" in the issue flow?
- How might we ensure the right notification reaches the right person at the right event — without creating notification noise?
- How might we allow flexibility in who can be notified (across teams) while keeping the assignee selection focused and meaningful?
- How might we let the Super Admin enable this feature once for an org without needing to configure it project by project?

---

**🤖 User Persona**

| Role | Context of Use | Goal | Frustration | Success |
|------|----------------|------|-------------|---------||
| Site Engineer / QC Inspector | On-site, mobile app, often in low-connectivity areas | Raise an issue and make sure the right people are looped in immediately | Has to manually call or message stakeholders after raising an issue | Issue raised, assignee notified instantly, relevant team members kept in the loop — no extra effort |
| Project Admin | Office or on-site, monitoring open issues across teams | Know that all relevant stakeholders are notified on every issue event | Updates are missed because only the assignee is notified | Every key event on an issue triggers the right notification to the right people automatically |
| Admin / Super Admin | Admin panel, initial org setup | Enable the feature once and have it work everywhere | Has to go into each project to configure features | Toggle turned on at org level; all projects in the org have it active immediately |

---

**📖 User Story**

> As a **Site Engineer / QC Inspector**, I want to assign an issue to one responsible person and optionally select additional people to be notified, so that everyone who needs to be aware of the issue gets informed automatically as it progresses.

> As an **Admin / Super Admin**, I want to control whether the assignment + notification feature is available in my organisation, so that it applies consistently to all projects without project-level configuration.

---

**✅ Acceptance Criteria**

**Super Admin Configuration**

- [ ] In the Super Admin panel, under Addon Services for an organisation, a toggle for "Issue Assignment & Notification" must be visible
- [ ] When this toggle is ON, the assignee + notification selection flow is available in all projects under that organisation
- [ ] When this toggle is OFF, the issue raising flow remains exactly as it is today — no changes to assignee selection, no notification recipient step, no UI changes of any kind
- [ ] The toggle state applies automatically to all projects in the org — no per-project configuration is needed
- [ ] Only Super Admins can see and change this toggle

**Assignee Selection**

- [ ] When raising an issue, the user must select exactly one assignee — this is mandatory
- [ ] The assignee list shows all users from all teams in the project, grouped by team with a team name section header above each group
- [ ] Users with the Associate role in the project must be excluded from the assignee list — they cannot be assigned an issue
- [ ] Each user row must show: full name, mobile number, and team name
- [ ] A search field must be available to find users by name, team, or mobile number
- [ ] "Phone Contact" option must be available on the assignee selection screen (to assign to a contact outside the platform)
- [ ] Only one person can be selected as assignee — selecting a new person deselects the previous selection

**Notification Recipient Selection**

- [ ] After selecting the assignee, the user sees an optional step to select notification recipients
- [ ] The notification recipient list is grouped into three sections: Assignee's Team, My Team (the assigner's team), and Other Teams
- [ ] In the Assignee's Team section: all users from the assignee's team are shown except those with the Associate role in the project
- [ ] In the My Team section: all users from the assigner's own team are shown except those with the Associate role in the project
- [ ] In the Other Teams section: only users who hold the Inspector role or Project Admin role in the project AND have project access are shown — all other roles from other teams are excluded
- [ ] Multiple recipients can be selected — there is no upper limit
- [ ] "Phone Contact" option must NOT be available on the notification recipient selection screen
- [ ] The notification selection step is optional — the user can skip it and proceed to raise the issue
- [ ] A search field must be available on this screen to find users by name, team, or mobile number
- [ ] Each listed user must show name, mobile number, and team name

**Final Raise Screen**

- [ ] Before raising the issue, the user sees a summary screen showing: Project, Location, Type, Tags, Recommendation, Deadline, Team, Team User (assignee name and mobile), Issue description, and attached photo(s)
- [ ] The summary screen must also show the list of selected notification recipients below the assignee section
- [ ] If 3 or fewer notification recipients are selected, each recipient is shown as a full row with name and mobile number
- [ ] If more than 3 notification recipients are selected, the first 2 are shown as full rows, followed by a collapsed row showing "+N more" — tapping it expands to show the full list
- [ ] If no notification recipients were selected, the Notified Users section is either hidden or shows "None"
- [ ] A "Raise" button is shown at the bottom to submit the issue
- [ ] The user can go back from this screen to change assignee or notification recipients before raising

**Notification Events**

The rule across all events: **the person who performed the action does not receive a notification. All other involved parties do.**

| Event | Action Taken By | Assigner | Assignee | Notified Users |
|-------|-----------------|----------|----------|----------------|
| Issue Raised | Assigner | — | Mobile Push + WhatsApp | Mobile Push |
| Responded | Assignee | Mobile Push + WhatsApp | — | Mobile Push |
| Rejected | Assigner | — | Mobile Push + WhatsApp | Mobile Push |
| Accepted | Assigner | — | Mobile Push + WhatsApp | Mobile Push |
| Closed | Assigner | — | Mobile Push + WhatsApp | Mobile Push |

- [ ] When an issue is **Raised** (action by Assigner): the Assignee receives Mobile Push + WhatsApp; Notified Users receive Mobile Push; the Assigner receives nothing
- [ ] When an issue is **Responded to** (action by Assignee): the Assigner receives Mobile Push + WhatsApp; Notified Users receive Mobile Push; the Assignee receives nothing
- [ ] When an issue is **Rejected** (action by Assigner): the Assignee receives Mobile Push + WhatsApp; Notified Users receive Mobile Push; the Assigner receives nothing
- [ ] When an issue is **Accepted** (action by Assigner): the Assignee receives Mobile Push + WhatsApp; Notified Users receive Mobile Push; the Assigner receives nothing
- [ ] When an issue is **Closed** (action by Assigner): the Assignee receives Mobile Push + WhatsApp; Notified Users receive Mobile Push; the Assigner receives nothing
- [ ] In every event, the person who performed that action must not receive any notification for that event — regardless of whether they are also listed as a Notified User
- [ ] If a Notified User / assigned User is also the action taker for a specific event, they must not receive a notification for that event — but must still receive notifications for all other events where they are not the action taker
- [ ] WhatsApp notifications are only sent if the WhatsApp Instruction addon is enabled for the organisation (based on existing Super Admin toggle)

**Role & Permission Behavior**

- [ ] Any user with project access who is raising an issue can use the assignee + notification selection flow (if the org-level toggle is ON)
- [ ] Users with the Associate role in the project cannot be assigned an issue and cannot appear in the assignee list
- [ ] Users with the Associate role in the project cannot be selected as a notification recipient in any section (Assignee's Team, My Team, or Other Teams)
- [ ] In the Other Teams section of notification recipients, only users holding the Inspector role or Project Admin role in the project with project access are shown

**States & Validations**

- [ ] If no assignee is selected and the user tries to proceed, the system must show a validation message — assignee is required
- [ ] If no notification recipients are selected and the user proceeds, the issue must be raised normally — no error
- [ ] If the org-level toggle is OFF, the entire issue raising flow remains exactly as the existing product — no new screens, no new steps, no UI changes appear anywhere

**Flow Continuity — What Happens Next**

- [ ] After raising the issue, the user is returned to the issue list or confirmation screen (existing behaviour)
- [ ] Notifications are sent immediately after the issue is raised — no delay
- [ ] The assigner can view the raised issue and see both the assigned person and the notification recipients listed on the summary screen before raising

---

**⚠️ Edge Cases & Constraints**

**Positive Cases**

- [ ] A user who selects an assignee and no notification recipients must be able to raise the issue successfully
- [ ] A user who selects both an assignee and multiple notification recipients must have all of them notified correctly — including Notified Users receiving Push on the Responded event
- [ ] A notification recipient from the Other Teams section (Inspector or Project Admin role) must receive Mobile Push for all events where they are not the action taker
- [ ] When more than 3 notification recipients are selected, the summary screen must show the first 2 and a "+N more" collapsed row — tapping it must expand to show the full list

**Negative Cases**

- [ ] A user with the Associate role must not appear in the assignee list or in any section of the notification recipient list
- [ ] The "Phone Contact" option must not be available on the notification recipient screen — if it appears, it is a bug
- [ ] If the Super Admin toggle is OFF for the org, the issue raising flow must be identical to the existing product — no new UI, no new steps
- [ ] A user who took the action on an event (e.g., the Assignee responding) must not receive a notification for that specific event — even if they are also listed as a Notified User

**Edge Cases**

- [ ] If the assignee's team has only Associate-role users aside from the assignee themselves, the Assignee's Team section in the notification recipient list shows an empty state — not an error
- [ ] If the assigner's own team has no other users, or all others are Associates, the My Team section shows an empty state
- [ ] If an issue is raised and then the assignee's account is deactivated before a response — the notification for the Responded event should still be sent to the Assigner
- [ ] A user who belongs to both the assignee's team and the assigner's team must only appear once in the notification recipient list — no duplicates across sections
- [ ] If exactly 3 notification recipients are selected, all 3 are shown as full rows on the summary screen — the "+N more" pattern only applies when the count exceeds 3

**How to Test**

- Test with Super Admin toggle ON and OFF — verify toggle OFF leaves the issue flow completely unchanged (no new screens, no new steps)
- Test assignee list: add an Associate-role user to a project and verify they do not appear in the assignee list or in any section of the notification recipient list
- Test that the assignee list groups users by team with a section header per team
- Test each event (Raised, Responded, Rejected, Accepted, Closed) — verify the action taker receives no notification for that event; all other involved parties receive the correct channel (Push and/or WhatsApp)
- Test Responded event specifically — verify Notified Users receive Mobile Push (this was not the case before)
- Test the "Phone Contact" option: verify it is visible on the assignee screen but absent on the notification recipient screen
- Test Other Teams section in notification recipients: add a user with Viewer or Associate role from another team — verify they do not appear; add one with Inspector or Project Admin role — verify they do appear
- Test summary screen with 1, 3, 4, and 10 notification recipients — verify the "+N more" collapsed row appears only when count exceeds 3, and tapping it expands correctly
- Test raising an issue with zero notification recipients — verify the issue is raised without error and the Notified Users section on the summary screen is hidden or shows "None"

---

# SECTION B — DESIGN PROMPT

---

**🎨 Design Prompt**

```
Screens: Issue Assignment — Assignee Selection, Notification Recipient Selection, Final Raise Summary
Platform: Mobile (iOS / Android)
Audience: Site QC Engineer / Field User — on-site use, outdoor lighting, gloved hands
Style: Clean, high contrast, large tap targets. digiQC design system.
       Dark navy CTA buttons. Rounded cards. Subtle separators.
       Search bar at top. Sectioned user list with team grouping.

--- SCREEN 1: Assignee Selection ---

Layout:
- Back arrow + "Assign Issue" title at top
- Search bar: "Find user by name, team, or mobile number"
- "Phone Contact" row — tappable option with right arrow (available on this screen only)
- Users listed grouped by team — each group has a bold section header with the team name, followed by users in that team
- Each user row: full name (bold), mobile number; single-select radio button on right
- "Back" and "Continue" buttons at bottom — Continue active only when one user is selected

States to show:
- Default: Grouped user list with search bar, no user selected, Continue button greyed out
- Selected: One row highlighted, radio filled, Continue button becomes active (dark navy)
- Empty: "No team users found" with prompt to search differently
- Search active: List filters in real time across all team groups

Pop-ups / Modals:
- No pop-ups on this screen

Role-based visibility:
- All raising users see the same screen — no role-based differences on the assignee list
- Associate-role users are never shown in any team group

Navigation / Next Step:
- Continue — goes to Notification Recipient Selection screen (if org toggle is ON)
- Back — returns to the previous issue form step

Notes:
- Associate-role users must NOT appear in any team group
- Phone Contact row is always shown above the team group list
- Only one radio can be selected at a time — tapping a new user auto-deselects the previous one
- Team section headers should be sticky while scrolling within that group

--- SCREEN 2: Notification Recipient Selection ---

Layout:
- Back arrow + "Notify People" title at top
- Subtitle: "Optional — select people to notify about this issue"
- Search bar: "Find user by name, team, or mobile number"
- NO "Phone Contact" option on this screen
- Three named sections with bold section headers:
    1. "Assignee's Team" — shows all team members except Associates
    2. "My Team" — shows all members of the assigner's team except Associates
    3. "Other Teams" — shows only users with Inspector or Project Admin role who have project access
- Each user row: name (bold), mobile number, team name; multi-select checkbox on right
- "Skip" text button (left) and "Continue" filled button (right) at bottom
- Continue is available at all times — even with 0 selections

States to show:
- Default: All three sections visible, all unchecked, Continue and Skip both visible
- Selected: One or more checkboxes filled, Continue active (dark navy), selected count shown (e.g. "3 selected")
- Empty section: "No eligible users" shown as a sub-row within that section — section header still visible
- Fully empty (all sections empty): "No users available to notify" with only Skip button shown
- Search active: List filters in real time across all three sections

Pop-ups / Modals:
- No pop-ups on this screen

Role-based visibility:
- "Other Teams" section only shows users with Inspector or Project Admin role and project access
- Associate-role users are never shown in any section regardless of team

Navigation / Next Step:
- Continue or Skip — goes to Final Raise Summary screen
- Back — returns to Assignee Selection screen

Notes:
- Phone Contact option must not appear anywhere on this screen
- A user who belongs to both Assignee's Team and My Team must only appear once — shown under Assignee's Team only

--- SCREEN 3: Final Raise Summary (Bottom Sheet / Modal) ---

Layout:
- "Issue" title with X close button at top right
- Scrollable label-value pairs listed vertically:
    Project:          [name]
    Location:         [breadcrumb e.g. Building - A/Hi]
    Type:             [e.g. Safety]
    Tags:             [#Tag1  #Tag2]
    Recommendation:   [text]
    Deadline:         [Day, DD Month HH:MM AM/PM]
    Team:             [assignee's team name]
    Team User:        [assignee name]
                      [mobile number]
    Notified Users:   [recipient 1 name — mobile]
                      [recipient 2 name — mobile]
                      [+N more →] (shown only if count > 3; tapping expands inline to show all)
    Issue:            [description text]
    [Photo thumbnail if attached — tappable to preview]
- "Raise" dark navy full-width button pinned at bottom

States to show:
- Default: All filled fields visible, Raise button active
- 0 notification recipients: Notified Users row shows "None" or is hidden
- 1–3 notification recipients: all shown as individual rows
- 4+ notification recipients: first 2 shown, then "+N more →" tappable row; tapping expands to show all inline
- No photo attached: Omit photo thumbnail row entirely
- After tapping Raise: button shows loading state briefly, then screen dismisses on success

Pop-ups / Modals:
- No confirmation pop-up before raising — Raise button submits directly

Role-based visibility:
- No role-based differences on this screen

Navigation / Next Step:
- Raise — submits the issue; user is taken back to the issue list (existing behaviour)
- X or Back — returns to Notification Recipient Selection screen

Notes:
- Both assignee and notification recipients are visible on this screen
- All fields shown are read-only — no editing on this screen
- Expanded "+N more" list should not open a new screen — it expands inline within the summary sheet
```

---

# SECTION C — RELEASE NOTE DETAILS

---

**📣 Release Note Details**

**Overview**
digiQC now lets field users choose who to notify when raising an issue — so the right people across all teams are automatically kept informed as the issue moves through its lifecycle, from raising to closure.

**Who Benefits & How**

- **Site Engineers / QC Inspectors:** Can loop in relevant team members when raising an issue — no need to manually call or message anyone after the fact
- **Project Admins:** All key stakeholders are automatically notified at each stage — better visibility without manual broadcasting
- **Assignees:** Receive an immediate push notification and WhatsApp message when they are assigned an issue — nothing gets missed
- **Org Admins / Super Admins:** Enable this feature once at the organisation level and it applies to all projects automatically

**What's New**

- Optional notification recipient selection when raising an issue
- Assignee list grouped by team for easier scanning and selection
- Three-section notification recipient list: Assignee's Team, My Team, and Other Teams (Inspector and Project Admin roles with project access)
- Smarter notification logic — the person who takes an action is never notified for that action; all other involved parties always are
- Notified Users now also receive a Mobile Push when the assignee responds to an issue
- Notification recipients shown on the final summary screen — with a "+N more" collapsed view when the list is long
- Org-level toggle in Super Admin panel to enable or disable the feature; toggle OFF leaves the existing flow completely unchanged
- Phone Contact option available for assignee selection but intentionally excluded from notification recipient selection

**How It Works**

When raising an issue, the field user first selects one assignee from a team-grouped list (mandatory). They then optionally choose one or more people to notify — from the assignee's team, their own team, or other project teams (Inspector and Project Admin roles only). The final summary screen shows both the assignee and all selected notification recipients before raising. Once raised, each person receives notifications based on who acted: the person who performed the action is never notified for that event — all others are. Notified Users receive a Mobile Push notification across all five events. The feature is controlled by the Super Admin and works across all projects in the organisation when enabled — with no impact on any project when the toggle is off.

---

**Interactive Prototype:**
- [View Live Screen](https://digiqc-hq.github.io/product-management/screens/us-issue-assignment-notification/)
- [View Source Code](https://github.com/digiqc-hq/product-management/blob/main/docs/screens/us-issue-assignment-notification/index.html)
