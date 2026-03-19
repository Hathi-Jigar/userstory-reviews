# Feature PRD — Checklist Bulk Actions

**🗂 User Story: Bulk Assign, Configure & Change Status on Checklist Listing**

**Module / Area:** Checklist / Settings — Project Level

**Type:** Feature Enhancement

**Interactive Prototype:**
- [View Live Screen](https://digiqc-hq.github.io/product-management/screens/us-checklist-bulk-actions/)
- [View Source Code](https://github.com/digiqc-hq/product-management/blob/main/docs/screens/us-checklist-bulk-actions/index.html)

---

## 📝 Brief Description

Admins managing large projects often need to roll out or update dozens of checklists at once. Today, doing this one-by-one is slow and prone to mistakes. This feature adds multi-select capability to the Checklist Listing page and enables three bulk operations: assign users to checklist, RFI, and approval roles; configure stage-level settings; and change checklist status (Go Live, Archive, Unarchive). All changes apply across all stages of each selected checklist.

---

## 🎯 Jobs to Be Done (JTD)

| Role | When… | They want to… | So they can… |
|------|--------|---------------|--------------|
| System Admin | Setting up a new project with 40+ checklists | Assign executors, approvers, and RFI users in one go | Avoid opening each checklist individually and reduce setup time |
| Project Admin | Rolling out checklists for a new phase | Push all relevant checklists to Live at once | Start inspections without delay and ensure all checklists are ready |
| Project Admin | Retiring a completed phase | Archive all checklists belonging to that phase together | Keep the project clean without affecting active work |
| System Admin | Applying a standard configuration across checklists | Turn on Drawing Required and Witness Required in bulk | Enforce org standards consistently without manual checklist-by-checklist edits |

---

## 💡 How Might We (HMW)

- How might we let admins act on many checklists at once without losing control of which checklists are affected?
- How might we guide admins through Go Live without blocking them — showing what is needed while still respecting their judgment?
- How might we design the bulk configuration drawer so admins only change what they intend to and leave everything else untouched?
- How might we give admins clear feedback on what succeeded, what was skipped, and why — especially when mixed-status selections are involved?
- How might we structure the Go Live flow so the path from selection to live is as short as possible for admins who are fully prepared?

---

## 👤 User Persona

| Role | Context of Use | Goal | Frustration | Success |
|------|----------------|------|-------------|---------|
| System Admin | Desktop, project setup phase, managing 30–60 checklists | Get all checklists assigned and live before site work begins | Has to open each checklist, navigate to settings, and repeat the same action dozens of times | All checklists assigned and live in under 5 minutes |
| Project Admin | Desktop, mid-project, rolling out a new inspection phase | Push a batch of checklists live with the right people assigned | Mixed statuses cause confusion — no way to act on a group at once | Selects the relevant checklists, assigns users, goes live — all in one flow |

---

## 📌 User Story

> As a **System Admin or Project Admin**, I want to select multiple checklists on the Checklist Listing page and bulk-assign users, configure stage settings, and change checklist status, so that I can manage many checklists at once without opening them one by one.

---

## ✅ Acceptance Criteria

---

### Roles & Permissions

- [ ] Only **System Admin** and **Project Admin** can see and use bulk selection and bulk action controls on the Checklist Listing page
- [ ] Checklist Maker and all other roles do not see checkboxes or the bulk action toolbar
- [ ] All bulk actions are scoped to the current project — no cross-project actions
- [ ] The backend validates the user's role and project scope before applying any bulk change

---

### Bulk Selection — Checkbox Column

- [ ] The Checklist Listing table includes a checkbox column as the first column
- [ ] Each row has an individual checkbox
- [ ] The column header has a **Select All on this page** checkbox
- [ ] Selecting the header checkbox selects all visible rows on the current page
- [ ] When at least one row is selected, a **bulk action toolbar** appears showing: **N selected** count, and action buttons: **Assign Users**, **Configure**, **Status**
- [ ] When the header checkbox is selected and there is **only one page** of results, all rows on the page are selected — no Quick Select dropdown appears
- [ ] When the header checkbox is selected and there are **multiple pages** of results, a **Quick Select dropdown** appears with two options:
  - **Select all on this page** — default, selects only the visible rows on the current page
  - **Select all across all pages (X total)** — shows the total count of checklists matching the active filters and selects all of them
- [ ] Selecting "Select all across all pages" updates the count in the toolbar to show the full filtered total (e.g., **47 selected**)
- [ ] "Select all across all pages" respects any active filters — it selects only filtered results, not every checklist in the project
- [ ] Deselecting any individual row after "Select all across all pages" reverts the selection back to manual mode
- [ ] Clearing the header checkbox deselects all rows and hides the bulk action toolbar

---

### Bulk Assignment — Toolbar Entry Point

- [ ] Clicking **Assign Users** on the bulk toolbar opens a dropdown with three options:
  - **Assign Checklist Users**
  - **Assign RFI Users**
  - **Assign Approver**
- [ ] Each option opens its own dedicated right-side drawer
- [ ] After an assignment drawer is closed, the system shows a prompt: *"Do you also want to set RFI Users / Approvers?"* — giving quick access to the next assignment type
- [ ] Admin can dismiss the prompt at any time — no assignment type is mandatory from the toolbar

---

### Bulk Assignment — Assign Checklist Users Drawer

- [ ] Opens as a right-side drawer when admin selects **Assign Checklist Users** from the Assign Users dropdown
- [ ] Drawer title: *"Assign Checklist Users (N Checklists Selected)"*
- [ ] An info banner reads: *"Only the current changes will be applied. All other assignments and configurations will remain unchanged."*
- [ ] The drawer has two tabs: **Assign** and **Remove**
- [ ] **Assign tab:** Admin selects users to add to all stages of the selected checklists
  - User list sourced from **project users** only
  - Searchable multi-select input with user name tags
- [ ] **Remove tab:** Shows all currently assigned project users as a list with checkboxes — admin selects users to remove
  - User list sourced from **project users** only
- [ ] Only one tab is active at a time — admin cannot Assign and Remove in the same action
- [ ] Assignment applies to **all stages** of each selected checklist equally
- [ ] The drawer has **Cancel** and **Save** buttons in the footer
- [ ] Clicking **Save** shows a confirmation pop-up: *"You are about to update Checklist User assignments for N checklists. This will affect all stages. Do you want to continue?"*
- [ ] On **Confirm**, changes are applied and a toast is shown: *"Checklist User assignments updated for N checklists"*
- [ ] If no users are selected in the active tab, the Save button is disabled

**Example — Assign tab:**
Admin selects 15 checklists and opens Assign Checklist Users. They pick Rajesh and Mehul from the project user list and click Save. Both users are added as executors to all stages of all 15 checklists. Any users already assigned to those stages remain unchanged.

**Example — Remove tab:**
Admin switches to the Remove tab. All currently assigned project users are listed with checkboxes. Admin selects Priya and clicks Save. Priya is removed from all stages of all 15 checklists. All other assigned users remain unchanged.

---

### Bulk Assignment — Assign RFI Users Drawer

- [ ] Opens as a right-side drawer when admin selects **Assign RFI Users** from the Assign Users dropdown
- [ ] Drawer title: *"Assign RFI Users (N Checklists Selected)"*
- [ ] An info banner reads: *"Only the current changes will be applied. All other assignments and configurations will remain unchanged."*
- [ ] The drawer has two tabs: **Assign** and **Remove**
- [ ] **Assign tab:** Admin selects users to add to all RFI stages of the selected checklists — user list sourced from project users only
- [ ] **Remove tab:** Shows all currently assigned RFI users as a list with checkboxes — admin selects users to remove
- [ ] Only one tab is active at a time
- [ ] Checklists that have no RFI stages are silently skipped — counted in the toast as Skipped
- [ ] The drawer has **Cancel** and **Save** buttons in the footer
- [ ] Clicking **Save** shows a confirmation pop-up: *"You are about to update RFI User assignments for N checklists. Do you want to continue?"*
- [ ] On **Confirm**, changes are applied and a toast is shown: *"RFI User assignments updated for N checklists | Skipped: X (no RFI stages)"*
- [ ] If no users are selected in the active tab, the Save button is disabled

**Example — Assign tab:**
Admin selects 20 checklists, 5 of which have no RFI stages. They open Assign RFI Users, pick Amit, and click Save. Amit is added to the RFI stages of the 15 checklists that have RFI. The 5 without RFI stages are skipped and shown in the toast.

**Example — Remove tab:**
Admin opens the Remove tab. All currently assigned RFI users are listed with checkboxes. Admin selects Farhan and clicks Save. Farhan is removed from RFI stages across all applicable checklists. All other RFI users remain unchanged.

---

### Bulk Assignment — Assign Approver Drawer

- [ ] Opens as a right-side drawer when admin selects **Assign Approver** from the Assign Users dropdown
- [ ] Drawer title: *"Assign Approver (N Checklists Selected)"*
- [ ] An info banner reads: *"Only the current changes will be applied. All other assignments and configurations will remain unchanged."*
- [ ] The drawer has two tabs: **Assign** and **Remove**
- [ ] The drawer contains **three level sections**: **Level 1**, **Level 2**, **Level 3**
- [ ] Each level section has two sub-sections: **Internal Approvers** and **External Approvers**
  - **Internal Approvers** — user list sourced from **project users**
  - **External Approvers** — user list sourced from **organisation users** (not limited to the project)
  - If an external user selected is already a project member, they are automatically moved to the **Internal Approvers** list on save — no duplicate entry is created
- [ ] **Assign tab:** Admin selects users to add as approvers at each level
- [ ] **Remove tab:** Shows all currently assigned approvers (Internal and External) per level with checkboxes — admin selects users to remove
- [ ] Only one tab is active at a time
- [ ] Admin can fill one, two, or all three levels — any level left empty is skipped (no change to that level)
- [ ] If a checklist stage has fewer than 3 approval levels configured, only the levels that exist are updated — extra level inputs in the drawer are ignored for that stage
- [ ] The drawer has **Cancel** and **Save** buttons in the footer
- [ ] Clicking **Save** shows a confirmation pop-up: *"You are about to update Approver assignments for N checklists. This will affect all applicable stages. Do you want to continue?"*
- [ ] On **Confirm**, changes are applied and a toast is shown: *"Approver assignments updated for N checklists"*
- [ ] If no users are selected across any level in the active tab, the Save button is disabled

**Example — Assign tab (Level 1 only):**
Admin selects 10 checklists and opens Assign Approver. They add Kiran (Internal) and Vinod Contractors (External) to Level 1, leave Level 2 and Level 3 empty, and click Save. Level 1 approvers are updated on all stages of the 10 checklists. Level 2 and Level 3 are untouched.

**Example — External user auto-reclassify:**
Admin selects Rahul Shah under External Approvers for Level 1. Rahul is already a project member. On save, the system moves Rahul to Internal Approvers for Level 1 automatically — no error, no duplicate.

**Example — Remove tab:**
Admin opens the Remove tab. All currently assigned approvers are listed per level with checkboxes. Admin selects Vinod Contractors from Level 1 and clicks Save. Vinod is removed as a Level 1 approver from all applicable stages. All other approver assignments remain unchanged.

---

### Bulk Stage Configuration — Checklist Stage Drawer

- [ ] Clicking **Configure** on the bulk toolbar opens the **Checklist Stage Settings** drawer directly — no sub-menu or dropdown
- [ ] Drawer title: *"Configure Checklist Stage Settings (N Checklists Selected)"*
- [ ] An info banner reads: *"Only settings explicitly set to ON or OFF will be applied. Unselected settings remain unchanged."*
- [ ] The drawer shows **four** settings rows:
  - Drawing Required
  - Witness Required
  - Allow Skip
  - Require Validate
- [ ] **RFI Allowed is not shown in this drawer** — it is a project-level configuration and cannot be changed at the checklist level. A note at the bottom reads: *"RFI Allowed is a project-level setting. Update it in Project Settings."*
- [ ] Each setting has two options: **ON** and **OFF**
- [ ] By default, no option is selected for any setting (both ON and OFF appear unselected)
- [ ] If admin does not select ON or OFF for a setting, that setting is left unchanged on all selected checklists
- [ ] Only settings where admin explicitly selects ON or OFF are changed — all others remain as they are
- [ ] The drawer has **Cancel** and **Apply** buttons in the footer
- [ ] Clicking **Apply** shows a confirmation pop-up: *"You are about to update stage settings for N checklists. This will affect all stages. Do you want to continue?"*
- [ ] On **Confirm**, changes are applied and a toast is shown: *"Stage settings updated for N checklists"*
- [ ] If no setting has been changed (all still unselected), the Apply button is disabled

**Example — partial update:**
Admin selects 12 checklists and opens Checklist Stage Settings. They set Drawing Required → ON and Allow Skip → OFF. They leave Witness Required and Require Validate untouched. On Apply, only Drawing Required is turned on and Allow Skip is turned off across all stages of the 12 checklists. The other two settings are not changed.

**Example — no change applied:**
Admin opens the drawer, does not select ON or OFF for any setting. The Apply button remains disabled — no changes are made.

---

### Bulk Status — Go Live

- [ ] Clicking **Status** on the bulk toolbar opens a dropdown with three options: **Go Live**, **Archive**, **Unarchive**
- [ ] Selecting **Go Live** opens a **Go Live hub modal** — it does not execute Go Live immediately
- [ ] The Go Live modal contains:
  - **Step pills** at the top: `1. Checklist Users → 2. RFI Users (if applicable) → 3. Approver (optional) → 4. Go Live`
    - Pill states: grey (pending) | orange (active / current) | green ✓ (done)
    - Approver pill is always marked as optional
  - **Three assignment cards** shown below the step pills — one per assignment type
  - Each card shows: icon, title, description, and an **Assign** button
  - RFI Users card is only shown if at least one selected checklist has RFI stages
  - A note below the cards reads: *"Approver assignment is optional and can be done after going live"*
- [ ] Clicking **Assign** on any card opens the corresponding right-side assignment drawer — the same drawer used from the bulk toolbar
- [ ] When an assignment drawer is closed, the Go Live modal reopens and refreshes automatically — the relevant card and step pill update to reflect the current assignment state
- [ ] **Checklist Users assignment is mandatory** — the Go Live button is disabled until all selected checklists (excluding already-Live and Archived) have Checklist Users assigned
- [ ] **RFI Users assignment is mandatory if any selected checklist has RFI stages** — the Go Live button remains disabled until RFI Users are also assigned for those checklists
- [ ] **Approver assignment is optional** — the Go Live button is never blocked by missing approver assignment
- [ ] The **Go Live button** is disabled with a tooltip: *"Complete Checklist Users and RFI Users assignment first"* — tooltip is visible on hover when the button is disabled
- [ ] Once all mandatory assignments are complete, the Go Live button enables automatically
- [ ] Clicking the **Go Live button** shows a final confirmation pop-up: *"You are about to make N checklists live. Do you want to continue?"*
- [ ] On **Confirm**, the modal closes, Go Live executes, the listing page refreshes, and a result toast appears: *"Live: X | Unchanged: Y | Skipped: Z"*
  - **Live** = successfully moved to Live status
  - **Unchanged** = already Live — no action taken
  - **Skipped** = Archived status — must be Unarchived first before going live
- [ ] Admin can close the Go Live modal at any time without executing Go Live — the checklist selection on the listing page remains active

**Example — all assignments already done:**
Admin selects 8 checklists, all with Checklist Users and RFI Users assigned. Opens Go Live modal — all required step pills are green, Go Live button is enabled. Admin clicks Go Live, confirms, done.

**Example — missing Checklist Users:**
Admin selects 10 checklists, 3 have no Checklist Users assigned. Opens Go Live modal — Checklist Users card is in warning state, step pill is orange, Go Live button is disabled. Admin clicks Assign on the Checklist Users card — Assign Checklist Users drawer opens. Admin assigns users and closes the drawer — the Go Live modal reopens and refreshes, Checklist Users card turns green, Go Live button enables. Admin clicks Go Live.

**Example — admin skips approver and goes live:**
Admin selects 5 checklists with all required assignments done but no approvers set. Opens Go Live modal — Checklist Users and RFI Users step pills are green, Go Live button is enabled. Admin ignores the Approver card and clicks Go Live directly. Approver can be assigned after going live.

---

### Bulk Status — Archive

- [ ] Selecting **Archive** shows a confirmation pop-up: *"You are about to archive N checklists. This will make them inactive. Do you want to continue?"*
- [ ] On Confirm, changes are applied
- [ ] Result toast: *"Archived: X | Unchanged: Y | Skipped: Z"*
  - **Archived** = successfully archived
  - **Unchanged** = already Archived
  - **Skipped** = Draft status — Archive is not a valid transition from Draft
- [ ] Checklists in **Draft** status are counted as Skipped in the toast

---

### Bulk Status — Unarchive

- [ ] Selecting **Unarchive** shows a confirmation pop-up: *"You are about to unarchive N checklists. They will be restored to Live status. Do you want to continue?"*
- [ ] On Confirm, checklists in Archived status are moved back to Live
- [ ] Result toast: *"Unarchived: X | Skipped: Z"*
  - **Skipped** = checklists not in Archived status (Draft, Live) — no action taken on them

---

### Mixed Status Selections

- [ ] Admin can select checklists of any combination of statuses (Draft, Live, Archived) in a single bulk action
- [ ] For status actions, the system applies the action only where it is valid for the current status of that checklist
- [ ] Invalid transitions are silently skipped and counted in the Skipped total of the result toast
- [ ] The result toast always shows the full breakdown so the admin knows exactly what happened

---

### Flow Continuity

- [ ] After any bulk action completes, the selection is cleared and the listing page returns to its normal unselected state
- [ ] The listing page reflects updated statuses and data immediately after a bulk action — no manual refresh needed
- [ ] If the admin closes a modal, drawer, or confirmation pop-up without confirming, no changes are applied and the selection remains active
- [ ] The bulk toolbar remains visible as long as at least one checklist is selected

---

### Audit Trail

- [ ] Every bulk action is logged with: timestamp, acting user, action type (Assign / Configure / Status), list of affected checklist IDs, and the values changed
- [ ] For bulk assignment: log records the assignment type (Checklist Users / RFI Users / Approver), the tab used (Assign or Remove), which level was affected (for approvers), and which users were added or removed
- [ ] For bulk configuration: log records which settings were changed and what value (ON or OFF) they were set to
- [ ] For bulk status: log records the old status and new status for each affected checklist
- [ ] Audit log is accessible to System Admin and Project Admin within the project scope

---

## ⚠️ Edge Cases & Constraints

### Positive Cases
- [ ] Admin selects 30 checklists of mixed status and clicks Go Live — checklists already Live are Unchanged, Archived ones are Skipped, Draft ones with complete mandatory assignments go Live
- [ ] Admin uses Assign tab in Assign Checklist Users — existing assigned users are retained and new users are added alongside them, no one is removed
- [ ] Admin opens Assign Approver drawer, fills only Level 1 Internal and Level 3 External, leaves Level 2 empty — Level 1 and Level 3 are updated across all stages; Level 2 is untouched
- [ ] Admin opens Checklist Stage Settings, sets only Drawing Required → ON, leaves all others unselected — only Drawing Required is updated across all stages of selected checklists
- [ ] Admin opens Go Live modal with all mandatory assignments already done — Go Live button is immediately enabled, no assignment steps needed

### Negative Cases
- [ ] A user with Checklist Maker role does not see checkboxes or the bulk toolbar — bulk actions are completely hidden
- [ ] Admin opens Assign Checklist Users drawer, does not select any users, and tries to Save — Save button is disabled, no action taken
- [ ] Admin opens Go Live modal with missing Checklist User assignments — Go Live button is disabled; admin must use the Assign button on the Checklist Users card before the button enables
- [ ] Admin opens Configure drawer but does not select ON or OFF for any setting — Apply button is disabled
- [ ] RFI Allowed is not available in the Configure drawer — it cannot be configured at the checklist level

### Edge Cases
- [ ] Admin selects "All across all pages" (47 checklists), then deselects 2 manually — the system reverts to manual selection of 45; bulk action applies to only those 45
- [ ] Admin selects an external approver in Assign Approver who is already a project member — on save, the system automatically moves them to Internal Approvers; no duplicate entry and no error shown to the admin
- [ ] Admin opens Assign RFI Users on a selection where 5 of 20 checklists have no RFI stages — only the 15 with RFI stages are updated; toast shows: *"RFI User assignments updated for 15 checklists | Skipped: 5 (no RFI stages)"*
- [ ] Admin opens Go Live modal, assigns Checklist Users via drawer (modal refreshes), then closes the Go Live modal without clicking Go Live — no status changes are applied; selection remains active
- [ ] Admin opens configure drawer, sets a toggle to ON, then changes it back to unselected before clicking Apply — Apply button disables again; no change applied for that setting
- [ ] All selected checklists are already Live when Go Live is triggered — Go Live button is enabled (mandatory assignments exist on all), admin confirms, toast shows: *"Live: 0 | Unchanged: N | Skipped: 0"*
- [ ] Admin selects a mix of checklists where some have RFI and some do not — RFI Users card and step pill appear in the Go Live modal; only the checklists with RFI stages require RFI User assignment before Go Live enables

### How to Test
- Test with System Admin and Project Admin — both should see bulk controls and drawers. Test with Checklist Maker — should see no checkboxes or toolbar.
- Test "Select all on this page" with only one page of results — verify Quick Select dropdown does not appear.
- Test "Select all across all pages" with filters active — verify count matches full filtered total, not all project checklists.
- Test Assign Checklist Users → Assign tab: add User A → verify added without removing existing users.
- Test Assign Checklist Users → Remove tab: verify all currently assigned users are shown as a list; select and remove User A → verify only User A is removed, all others unchanged.
- Test Assign Approver with only Level 1 filled — verify Level 2 and Level 3 are unchanged across all selected checklists.
- Test external approver who is already a project member — verify they are moved to Internal automatically on save, no duplicate created.
- Test Checklist Stage Settings: set one toggle ON, one OFF, leave two unselected — verify only those two change. Verify RFI Allowed is not shown.
- Test stage config with no setting selected — verify Apply is disabled.
- Test Go Live modal: select checklists with missing Checklist Users — verify Go Live button is disabled. Assign users via drawer, close drawer, modal refreshes — verify button enables.
- Test Go Live modal: all mandatory assignments done, no approver — verify Go Live button is enabled immediately (approver is optional, never blocks).
- Test Go Live modal: close without clicking Go Live — verify no status changes, selection stays active.
- Test Go Live: select checklists with and without RFI — verify RFI Users card and pill appear; verify Go Live button only enables after both Checklist Users and RFI Users are assigned.
- Test mixed-status selection for Archive — verify Draft checklists are Skipped and toast shows correct breakdown.
- Test Unarchive on a selection that includes Draft and Live checklists — verify only Archived ones are unarchived, others are Skipped.

---

## 🎨 Design Prompt

```
Screen: Checklist Listing Page — Bulk Actions
Platform: Web (desktop)
Audience: System Admin, Project Admin — office/desktop use
Style: Clean, professional data table UI. digiQC design system.
       Brand color #FC5027. Font: Rubik. Minimal chrome.

Layout:

1. CHECKLIST LISTING TABLE
   - First column: Checkbox (individual row + header Select All checkbox)
   - Remaining columns: Checklist Name | Assigned User (Checklist) | Assigned User (RFI) | Assigned Team | Status | Actions
   - Status badges: Draft (grey) | Live (green) | Archived (muted orange)
   - Selected rows tinted light orange (#FC5027 at low opacity)

2. BULK ACTION TOOLBAR (appears when ≥1 row selected)
   - Left: "N selected" count label
   - Buttons: [Assign Users ▾] [Configure] [Status ▾]
   - Configure opens drawer directly — no dropdown
   - Right: [×] Clear selection

3. QUICK SELECT DROPDOWN (only when multiple pages exist)
   - Option 1: Select all on this page
   - Option 2: Select all across all pages (X total)

4. ASSIGN USERS DROPDOWN
   - Three options: Assign Checklist Users | Assign RFI Users | Assign Approver
   - Each opens a right-side drawer

4a. ASSIGN CHECKLIST USERS DRAWER
   - Title: "Assign Checklist Users (N Checklists Selected)"
   - Blue info banner
   - Two tabs: [Assign] [Remove]
   - Assign tab: Searchable multi-select, project users only, user name tags
   - Remove tab: List of all currently assigned users
     - Each row: Avatar | Name | User type | Checkbox on right
   - Footer (sticky): [Cancel] [Save] — Save disabled if no users selected

4b. ASSIGN RFI USERS DRAWER
   - Same layout as Assign Checklist Users
   - Title: "Assign RFI Users (N Checklists Selected)"

4c. ASSIGN APPROVER DRAWER
   - Title: "Assign Approver (N Checklists Selected)"
   - Blue info banner
   - Two tabs: [Assign] [Remove]
   - Assign tab: Three expandable level sections (Level 1 | Level 2 | Level 3)
     - Each level: Internal Approvers (project users) + External Approvers (org users)
   - Remove tab: All currently assigned approvers per level with checkboxes
   - Footer (sticky): [Cancel] [Save]

5. CONFIGURE DRAWER (opens directly — no sub-menu)
   - Title: "Configure Checklist Stage Settings (N Checklists Selected)"
   - Blue info banner
   - Four setting rows: Drawing Required | Witness Required | Allow Skip | Require Validate
   - Each row: Setting label + description on left | [ON] [OFF] pills on right
   - ON / OFF both unselected by default
   - Note at bottom: "RFI Allowed is a project-level setting. Update it in Project Settings."
   - Footer (sticky): [Cancel] [Apply] — Apply disabled until at least one setting selected

6. STATUS DROPDOWN
   - Three options: Go Live | Archive | Unarchive

7. GO LIVE HUB MODAL
   - Title: "Go Live" | Subtitle: "N checklists selected" | Close (×) button
   - Step pills row below title:
     1. Checklist Users → 2. RFI Users (only if RFI checklists selected) → 3. Approver (optional) → 4. Go Live
     - Pill states: grey = pending | orange = active/required | green ✓ = done
     - Approver pill: always purple tint with "(optional)" label
   - Assignment cards (stacked vertically):
     - Each card: Icon | Title | Description | [Assign] button
     - Checklist Users: orange border + bg when missing, green when done
     - RFI Users: same — shown only if RFI checklists in selection
     - Approver: neutral grey border always | Assign button always shown
   - Note below cards (info icon): "Approver assignment is optional and can be done after going live"
   - Footer: [Cancel] [Go Live]
     - Go Live: disabled + greyed out when mandatory assignments missing
     - Tooltip on disabled: "Complete Checklist Users and RFI Users assignment first"
     - Go Live: enabled (orange) when all mandatory assignments done

8. CONFIRMATION POP-UPS (all bulk actions)
   - Centred modal: icon + message + [Cancel] [Confirm]
   - Confirm button in #FC5027

9. RESULT TOAST
   - Bottom-right: e.g. "Live: 18 | Unchanged: 4 | Skipped: 1"
   - Auto-dismiss after 5 seconds

States to show:
- Default: Table with checkboxes, no selection, no toolbar
- Selection active: Toolbar appears, selected rows tinted orange
- Drawer open: Table visible behind overlay, drawer slides in from right
- Loading: Save/Apply shows spinner, inputs locked
- Success: Drawer/modal closes, toast appears, selection clears, table refreshes
- Error: Toast — "Something went wrong. Please try again."
- Go Live button disabled: greyed out with tooltip visible on hover
- Go Live button enabled: orange, ready to click

Role-based visibility:
- System Admin and Project Admin: Full bulk controls visible
- All other roles: No checkboxes, no toolbar — read-only listing

Navigation / Next Step:
- After bulk action: drawer/modal closes, selection clears, listing refreshes
- Cancel on any drawer: no changes, selection stays active
- Go Live modal — drawer assignment: modal reopens and refreshes after drawer closes
- Post-assignment close (from toolbar): prompt shown to open next assignment drawer
```

---

## 📣 Release Note Details

**Overview**
Admins can now select multiple checklists on the Checklist Listing page and assign users, update stage settings, and change status in bulk — without opening each checklist individually.

**Who Benefits & How**
- **System Admin:** Can set up an entire project's checklists — assignments, settings, and live status — in minutes instead of hours.
- **Project Admin:** Can roll out or retire batches of checklists for a phase in a single action, with clear feedback on what changed and what was skipped.

**What's New**
- Multi-select with checkbox column on the Checklist Listing page
- Select all on page, or select all across all pages (filter-aware, only shown when multiple pages exist)
- Three dedicated assignment drawers — Assign Checklist Users, Assign RFI Users, Assign Approver — each with Assign and Remove tabs
- Remove tab shows all currently assigned users as a checkbox list — no free-form input needed
- Approver drawer covers all three approval levels, each with Internal (project users) and External (org users) sections
- External approvers who are already project members are automatically moved to Internal on save
- Bulk Stage Configuration opens directly from the toolbar (no sub-menu) — four settings: Drawing Required, Witness Required, Allow Skip, Require Validate. RFI Allowed is a project-level setting and is not editable here.
- Only the settings explicitly set to ON or OFF are applied — everything else remains untouched
- Bulk Status actions — Go Live, Archive, and Unarchive
- Go Live hub modal with step pills — Checklist Users and RFI Users are required before Go Live; Approver is always optional and never blocks
- Go Live button is disabled until mandatory assignments are complete; enables automatically when all required steps are done
- Result toast after every bulk action showing counts for changed, unchanged, and skipped checklists

**How It Works**
Select one or more checklists using the checkboxes on the Checklist Listing page. A toolbar appears with Assign Users, Configure, and Status options. Use Assign Users to open assignment drawers for Checklist Users, RFI Users, or Approver — each drawer has Assign and Remove tabs. Click Configure to open the stage settings drawer directly. For Go Live, the hub modal shows the assignment status for each type, with step pills that turn green as you complete each one. Checklist Users and RFI Users (where applicable) must be assigned before you can go live — Approver can be done at any time after.
