# 🗂 User Story: RFI Auto-Numbering with 7-Level Configurator

**Module / Area:** RFI / Project Settings / Super Admin — Addon Services

**Type:** New Feature

**Version:** v3.0 — Final

**Interactive Prototype:**
- [View Live Screen](https://digiqc-hq.github.io/product-management/screens/us-rfi-auto-numbering/)
- [View Source Code](https://github.com/digiqc-hq/product-management/blob/main/docs/screens/us-rfi-auto-numbering/index.html)

---

## 📝 Brief Description

digiQC needs a structured, configurable auto-numbering system for RFIs (Request for Inspection) that generates unique, sequential identifiers for every RFI raised in a project. A System Admin can configure a numbering format — built from up to 7 selectable levels — at any point as long as RFI is enabled for the project and no RFI has been raised yet. Once the first RFI is raised, the format is permanently locked. This eliminates ad-hoc or duplicate RFI references that currently hinder traceability and audit readiness on large construction projects.

---

## 🎯 Jobs to Be Done (JTD)

| Role | When… | They want to… | So they can… |
|------|--------|---------------|--------------|
| Super Admin (digiQC) | Managing an organisation's feature access | Enable RFI and RFI Auto-Numbering for eligible organisations | Ensure only qualifying projects can use auto-numbering and prevent ungoverned setups |
| System Admin | Setting up a new project or updating an existing one with RFI enabled | Configure a meaningful RFI numbering format using standard project identifiers | Ensure every RFI in the project carries a consistent, traceable identity |
| Project Manager / Quality Head | Reviewing or auditing RFIs across checklists and stages | Quickly locate and reference any RFI by its unique number | Trace quality issues, communicate with site teams, and present clean records to clients |
| Site Engineer / QC Inspector | Raising or tracking RFIs from mobile | See a clear RFI identifier on every inspection and stage screen | Communicate unambiguously with supervisors and avoid confusion across checklists |

---

## 💡 How Might We (HMW)

- How might we guide System Admins through format configuration so the format they set reflects how their organisation refers to RFIs in practice?
- How might we make the RFI numbering configurator easy to find without forcing it on the admin at a specific step?
- How might we communicate the format lock clearly enough that admins make deliberate, confident choices before saving?
- How might we handle segments that are conditionally absent (e.g., Reference Number not set on a checklist) without breaking the sequence logic?
- How might we surface RFI numbers consistently across Web, Mobile, and PDF so field teams and auditors always see the same identifier?

---

## 👤 User Persona

| Role | Context of Use | Goal | Frustration | Success |
|------|----------------|------|-------------|---------|
| Super Admin (digiQC) | Web, org settings panel, before client onboarding | Enable RFI Auto-Numbering for eligible orgs | Clients enable RFI without configuring numbering, leading to inconsistent identifiers | Every RFI-enabled project has access to a numbering configurator before field use begins |
| System Admin | Web, project settings page, any time before first RFI is raised | Configure a meaningful RFI number format that reflects project naming conventions | No standard format exists — teams invent ad-hoc identifiers that clash across checklists | Format saved, live preview confirmed, and field teams see consistent RFI numbers from day one |
| Project Manager / Quality Head | Web dashboard and PDF reports during audits | Locate and reference specific RFIs quickly by number | RFI references are inconsistent — some have names, some have checklist codes, no single format | Every RFI in every report carries the same structured identifier |
| Site Engineer / QC Inspector | Mobile app, on-site during inspection | See RFI number clearly on each inspection stage screen | RFI tracking requires manual cross-referencing with the office team | RFI number visible on screen immediately after raising; no ambiguity in communication |

---

## 📌 User Story

> As a **Super Admin**, I want to enable RFI Auto-Numbering at the organisation level so that any project with RFI turned ON can be configured with a numbering format by the System Admin.

> As a **System Admin**, I want to configure an RFI numbering format using up to 7 levels at any point before the first RFI is raised, so that every RFI in this project gets a unique, sequential, and standardised identifier visible across Web, Mobile, and PDF.

> As a **Project Manager or Quality Head**, I want to view the configured RFI numbering format in read-only mode, so that I understand the identifier structure used across all RFIs in the project.

---

## ✅ Acceptance Criteria

### A. Feature Enablement — Super Admin Control

- [ ] A toggle labelled **"RFI Auto-Numbering"** must be present in the Super Admin organisation settings panel, in the Addon Services section
- [ ] The toggle must appear immediately after the existing **"RFI"** toggle (item 11 in the current list), labelled as item **11a**
- [ ] The toggle is **OFF by default** for all organisations
- [ ] The toggle is only actionable if the **RFI feature is already enabled** for that organisation at Super Admin level; if RFI is OFF, the RFI Auto-Numbering toggle must remain disabled and non-interactive
- [ ] If RFI is turned OFF at Super Admin level, the RFI Auto-Numbering toggle must also be turned OFF automatically and hidden
- [ ] There is **no project-level toggle** for this feature — it is controlled exclusively at the Super Admin level
- [ ] When the Super Admin enables this toggle, the setting is stored against the organisation and immediately applies to all projects within that org that have RFI enabled

### B. Configurator Access — Who Can Open It

- [ ] The RFI Numbering Configurator is **accessible only to System Admins** for configuration and editing
- [ ] **Project Admins and Super Admins can view the configurator in read-only mode** after it has been saved; they cannot edit it
- [ ] Site Engineers, QC Inspectors, and Project Managers have no access to the configurator at all — the configurator option must not be visible to them
- [ ] The configurator is accessible from the **project settings page** at any point — it is not forced open at a specific step in the project flow

### C. Configurator Visibility — Project Level

- [ ] The RFI Numbering Configurator section must only appear on the project settings page **when RFI is turned ON** for that project
- [ ] If RFI is OFF in the project permissions, the configurator section must be hidden entirely; a neutral message must be shown instead: *"RFI Auto-Numbering is not available. Turn RFI ON to configure a numbering format for this project."*
- [ ] When RFI is toggled ON in the project permissions, the configurator section must appear immediately without a page reload
- [ ] When RFI is toggled OFF in the project permissions, the configurator section must hide immediately

### D. Configurator Access — When It Can Be Opened

- [ ] The configurator can be opened at **any stage** — during initial project setup or after the project is already created — as long as RFI is ON for the project and no RFI has been raised yet
- [ ] If no format has been saved yet, the configurator opens in **blank mode** with all levels empty
- [ ] If a format was previously saved but no RFI has been raised yet, the configurator opens in **edit mode** showing the previously saved format
- [ ] If the first RFI has already been raised, the configurator opens in **locked, view-only mode** — no editing is possible

### E. Configurator Rules — Format Definition

- [ ] The configurator must support **up to 7 levels** (Level 1 to Level 7); it is not mandatory to use all 7
- [ ] At least **1 level must be selected** before the format can be saved
- [ ] The **separator between all levels is fixed as `/`** and cannot be changed by the user
- [ ] The **same level option cannot be selected more than once** across the 7 levels; if a level is already selected, it must appear disabled in the dropdown for all other level rows
- [ ] If a selected text segment contains a space, the space must be **automatically replaced with `_`** in the generated number
- [ ] The following options must be available for selection at each level:

| Option | Sample Output | Notes |
|--------|---------------|-------|
| Project Name | `Megatrone` | Spaces replaced with `_` |
| Project Code | `MGT` | |
| Checklist Name | `RCC_Slab` | Spaces replaced with `_` |
| Checklist Stage | `During` | |
| Reference Number | `[Ref]` | Silently skipped if not set on the checklist |
| Full Date | `24012026` | Format: DDMMYYYY, project timezone |
| Time | `22:00` | Format: HH:MM 24-hour, project timezone |
| Number | `1` | Auto-increment; configurable start value, minimum: 1 |
| Year | `2026` | Format: YYYY, project timezone |
| Month | `01` | Format: MM, project timezone |
| Date | `24` | Format: DD, project timezone |
| Long Date | `24-01-2026` | Format: DD-MM-YYYY; uses `-` internally, no conflict with `/` level separator |
| Nomenclature Level | `Building_A` | L1 to L7, individually selectable; only available if Nomenclature is enabled for the org |

- [ ] All date and time values must use the **project's configured timezone**
- [ ] **Nomenclature Level options (L1–L7)** must only be available if the Nomenclature feature is enabled for the organisation
- [ ] If Nomenclature is **not enabled**, Nomenclature options must appear **greyed out and disabled** in the dropdown; the optgroup must be labelled to indicate they are inactive (e.g., *"Nomenclature Levels (inactive)"*); hovering the dropdown must show a tooltip: *"Nomenclature is not active for this organisation. Enable it in Super Admin → Addon Services."*
- [ ] **Number padding is not allowed** — the auto-increment counter must display as `1, 2, 3` — never `001, 002, 003`
- [ ] When **"Number"** is selected as a level, a **start value input field** must appear below it; the default start value is `1`; the System Admin can change it to any positive integer before the format is saved; once saved, the start value is locked along with the format

### F. Live Preview

- [ ] While the user configures levels, the configurator must display a **live preview** of the generated RFI number using sample values
- [ ] The preview must **update immediately** whenever the user adds, removes, or changes a level
- [ ] Sample values must reflect the options defined in Section E
- [ ] If Reference Number is selected, the preview must show a placeholder: `[Ref]` to indicate it is conditional
- [ ] If no valid level is selected, the preview must show: *"Select at least one level to see a preview"*

### G. Save Confirmation and Edit Lock

- [ ] On clicking **"Save Format"**, a confirmation modal must appear before saving:
  - **Title:** `Confirm RFI Numbering Format`
  - **Message:** `"This format will be used for all RFIs in this project. You can edit it until the first RFI is raised, after which it will be permanently locked. Do you want to continue?"`
  - **Buttons:** `Confirm & Save` (primary, brand colour #FC5027), `Cancel` (secondary)
- [ ] After confirmation, the format is saved and the configurator closes; a success toast must appear: *"RFI numbering format saved successfully."*
- [ ] The saved format is **editable by System Admin only** until the first RFI is raised in that project
- [ ] Once the **first RFI is raised**, the configurator transitions to a **locked, view-only state** permanently
- [ ] In the locked state, an **amber info banner** must display: *"RFI numbering format is locked because RFIs have already been raised for this project."*
- [ ] The locked configurator must display the configured format for reference — no edit controls are shown

### H. RFI Number Generation — Sequence Rules

- [ ] The RFI number sequence is **project-level** and increments globally, regardless of checklist type or stage
- [ ] Every RFI raised in the project receives the **next available sequential number**, starting from the configured start value
- [ ] All RFIs across all checklists and all stages in a project follow a **single global sequence** — there is no per-checklist or per-stage numbering
- [ ] The RFI number is assigned at the **point of server sync** — not when the RFI is created locally on mobile
- [ ] If two RFIs are raised simultaneously (e.g., offline and synced together), the one that reaches the server first receives the earlier number; the system must ensure **no two RFIs in the same project share an RFI number**

### I. Rejected RFI Behaviour

- [ ] A rejected RFI must **retain its original RFI number** — it is never reassigned, removed, or reused
- [ ] When a reinspection or new RFI is raised following a rejection, it must receive a **new incremental RFI number**; it does not reuse the rejected RFI's number

### J. Super Admin Toggle — Turned OFF After Projects Are Live

- [ ] If the Super Admin turns **RFI Auto-Numbering OFF** for an organisation after projects are already active:
  - All **previously generated RFI numbers remain unchanged** on existing RFIs
  - The configurator for all existing projects becomes **view-only** — no new configuration or edits are possible
  - **No new RFI numbers are generated** for any RFI raised after the toggle is turned OFF
  - RFIs raised after the toggle is OFF have **no auto-number** assigned
- [ ] If the Super Admin turns the toggle **back ON**, the configurator becomes editable again for projects where no RFI has been raised yet; projects with raised RFIs remain locked

### K. Backend Override

- [ ] A backend override option exists for use by **digiQC internal team only** — this is not accessible from the product UI
- [ ] The backend override allows the format to be changed even after the first RFI has been raised
- [ ] **Previously generated RFI numbers are never modified** when a backend override is applied — they retain their original assigned number
- [ ] New RFIs raised after the backend override use the new format and continue the sequence from the next available number
- [ ] Every backend override must be logged with: timestamp, who made the change, previous format, and new format

### L. Visibility — Web, Mobile, and PDF

- [ ] **Web — RFI Stage Detail Screen:** RFI Number must be displayed prominently on the RFI detail view
- [ ] **Web — Inspection Stage (associated stage view):** RFI Number must be visible for the stage associated with that RFI
- [ ] **Web — Project EQC Tab and Log EQC Tab (List Screen):** If the current or associated stage is RFI, the RFI Number must appear in the Location column, below the EQC name
  - Format example: `Building A / Ground Floor / C1 to C10 → RFI No: MGT/RCC_SLAB/2026/5`
  - The RFI Number in this list must be **searchable** via the search bar
- [ ] **PDF Reports — Stage Report, Final Report, Detailed Report:** RFI Number must appear in all three report types, associated with both the RFI stage and the inspection stage linked to that RFI
- [ ] **Mobile — Inspection stage screens and RFI detail screens:** RFI Number must be clearly visible; no configuration is possible from mobile

---

## ⚠️ Edge Cases and Constraints

**Positive Cases**
- [ ] System Admin opens the configurator on a new project, selects 4 levels including Number with start value 100, saves — first RFI raised must be numbered 100, second must be 101
- [ ] A project with 5 checklists and 3 stages each — all RFIs across all checklists and stages follow a single sequential number (e.g., 1, 2, 3 — not 1, 1, 1 per checklist)
- [ ] A checklist with no Reference Number set — if Reference Number is a configured level, that segment must be silently skipped for that checklist's RFIs; the rest of the format must remain intact and the sequence must not break

**Negative Cases**
- [ ] A Project Admin or Site Engineer attempts to open the configurator — the option must not be visible to them; if accessed directly via URL, a permission error must be shown
- [ ] System Admin attempts to save a format with 0 levels selected — save must be blocked; validation message: *"Please select at least one level to define the format."*
- [ ] System Admin selects the same level option in two rows — the duplicate must be disabled in the dropdown and not selectable
- [ ] System Admin attempts to edit a locked configurator — no edit controls must be shown; the amber lock banner must be displayed

**Edge Cases**
- [ ] RFI is turned OFF in project permissions — the entire configurator section must disappear from the project settings page immediately
- [ ] RFI is turned ON in project permissions — the configurator section must appear immediately without page reload
- [ ] RFI Auto-Numbering toggle is ON at Super Admin level, but System Admin has not yet configured a format — RFIs can still be raised but will have no auto-number until a format is configured and at least one RFI is raised after configuration
- [ ] Two RFIs synced simultaneously from offline — server must assign sequential numbers without conflict; no two RFIs in the same project may share a number
- [ ] Super Admin turns org-level toggle OFF then back ON — existing locked project configurators must remain locked; projects with no RFIs raised must be configurable again
- [ ] Nomenclature is disabled for an org but a previously saved format included a Nomenclature level — the saved format must continue to generate RFI numbers correctly; Nomenclature levels must only be greyed out for new configurations or edits going forward
- [ ] Long Date level selected — output uses `DD-MM-YYYY` with `-` as internal separator; this does not conflict with the `/` level separator in the final RFI number

**How to Test**
- Test as System Admin on a new project: open configurator — verify all 13 level options appear, Nomenclature group is available, live preview updates on every change, save confirmation modal appears before saving
- Test as Project Admin on the same project: verify configurator is visible in read-only mode with no dropdowns or save button
- Test as Site Engineer: verify the configurator section is not visible anywhere
- Test with Nomenclature disabled at Super Admin level: open configurator — verify L1–L7 optgroup is labelled as inactive, all Nomenclature options are greyed out and disabled, tooltip shows on hover
- Test RFI toggle OFF on project: verify configurator section hides and the neutral message appears; toggle RFI back ON — verify configurator section reappears
- Test format lock: raise one RFI, then open the configurator — verify amber locked banner appears, no edit controls shown, format is still visible for reference
- Test Reference Number omission: use a checklist with no Reference Number set and include Reference Number as a level — verify segment is silently skipped and the RFI number generates correctly for that checklist
- Test org toggle OFF: turn RFI Auto-Numbering OFF at Super Admin level — verify existing RFI numbers on past RFIs are unchanged, and new RFIs do not receive auto-numbers
- Test simultaneous offline sync: raise two RFIs offline and sync together — verify each receives a unique sequential number with no duplicate

---

## 🎨 Design Prompt

```
Screen: RFI Auto-Numbering — Two screens
Platform: Web (desktop), mobile responsive
Audience:
  Screen 1 — Super Admin Panel (digiQC internal)
  Screen 2 — Project Settings: Edit Project (System Admin)
Style: Clean, minimal. digiQC design system. Brand colour #FC5027. Font: Rubik.

─────────────────────────────────
SCREEN 1 — SUPER ADMIN: ORG DETAILS
─────────────────────────────────
Layout:
- Top nav: digiQC logo, nav items (Organizations, SuperAdmins, Gallery)
- Breadcrumb: Organisation name with Deactivate and Edit buttons
- Tabs: Details | Users
- Three-column grid: Org Info | Subscription Details | Addon Services

Addon Services panel:
- Existing toggles 1–15 as per current list
- Item 11: RFI toggle (existing)
- Item 11a: RFI Auto-Numbering toggle — appears only when item 11 (RFI) is ON
  - NEW badge next to label
  - Toggle is OFF by default
  - If RFI (item 11) is turned OFF, item 11a hides and its toggle resets to OFF
- Item 8: Nomenclature toggle — controls availability of L1–L7 in the configurator

States to show:
- RFI OFF: item 11a hidden
- RFI ON, Auto-Numbering OFF: item 11a visible, toggle is OFF
- RFI ON, Auto-Numbering ON: item 11a visible, toggle is ON
- Nomenclature toggled OFF: reflected downstream in configurator

Toast messages:
- Enabling RFI: "✓ RFI enabled. You can now enable RFI Auto-Numbering below."
- Disabling RFI: "RFI disabled. RFI Auto-Numbering has also been turned off."
- Enabling RFI Auto-Numbering: "✓ RFI Auto-Numbering enabled. System Admins can now configure it per project."
- Disabling RFI Auto-Numbering: "RFI Auto-Numbering disabled. Existing RFI numbers are preserved."
- Disabling Nomenclature: "⚠️ Nomenclature disabled. L1–L7 levels will be greyed out in the RFI configurator."

─────────────────────────────────
SCREEN 2 — PROJECT SETTINGS: EDIT PROJECT
─────────────────────────────────
Layout:
- Top nav: Organisation logo, nav items, System Admin avatar
- Breadcrumb: Project name > Edit Project
- Scenario bar: pills to switch between 5 states (prototype navigation only)
- Two-column grid: Project Details card | Site Details card

Project Details card:
- Standard fields: Name, Unique Code, Client Name, Description
- Permissions row: Location toggle, Authentication toggle, RFI toggle
- Divider
- RFI Numbering Format section — shown only when RFI toggle is ON:
  - Section label with status tag (Not Configured / Configured / Locked)
  - Config trigger card: dashed orange border, icon, title, subtitle, and arrow
  - Info/warning banners depending on state

States to show on project card (5 scenarios):

1. RFI OFF:
   - No configurator section shown
   - Grey neutral message: "RFI Auto-Numbering is not available. Turn RFI ON in Permissions above."
   - Turning RFI toggle ON must reveal the configurator section immediately

2. RFI ON · Not Configured:
   - Status tag: "Not Configured" (red)
   - Config trigger card with dashed orange border
   - Title: "Configure RFI Numbering Format"
   - Subtitle: "Set up before the first RFI is raised"

3. RFI ON · Configured (editable):
   - Status tag: "✓ Configured" (green)
   - Blue info banner: "Format is active. You can still edit it until the first RFI is raised."
   - Config trigger shows saved format (e.g., MGT / RCC_Slab / 2026 / 1)
   - Edit icon on trigger

4. RFI ON · Locked:
   - Status tag: "🔒 Locked" (grey)
   - Config trigger with grey/disabled styling and lock icon
   - Subtitle: "Locked — RFIs have been raised · tap to view"
   - Eye icon on trigger

5. RFI ON · Nomenclature Inactive:
   - Same as Not Configured state
   - Amber warning banner: "Nomenclature is not active for this organisation. L1–L7 levels will be disabled in the configurator."

─────────────────────────────────
CONFIGURATOR MODAL
─────────────────────────────────
Opened from: Project Settings config trigger card
Max width: 680px, scrollable

Modal header:
- Title: "RFI Numbering Format"
- Subtitle: Project name · Role label
- When Nomenclature is inactive: small amber chip in header: "⚠️ Nomenclature Inactive — hover for info"
  with tooltip: "Nomenclature L1–L7 is not active. Enable in Super Admin → Addon Services."

Modal body:
- Locked banner (amber): shown when format is locked
- Edit info banner (blue): shown when format is editable
- Levels section: up to 7 level rows, each with:
  - Level number badge (dark circle)
  - Dropdown with grouped options: Project | Checklist | Date & Time | Sequence | Nomenclature Levels
  - Nomenclature optgroup: labelled "⊘ Nomenclature Levels (inactive)" when inactive; all options greyed out
  - Tooltip on dropdown hover when nom is inactive: "Nomenclature is not active. Enable in Super Admin → Addon Services."
  - Number level: shows start value input below dropdown (default: 1)
  - Remove (×) button on each row
- "+ Add Level" button (disabled at 7 levels)
- Divider
- Live Preview section:
  - Label: "Generated RFI Number"
  - Format displayed in large bold text: MGT / RCC_Slab / 2026 / 1
  - [Ref] placeholder shown for Reference Number level
  - Placeholder text when no levels selected

Modal footer (edit mode only):
- Cancel (secondary)
- Save Format (primary, #FC5027) — disabled until at least 1 valid level is selected

Locked state:
- All level rows show read-only chips instead of dropdowns
- Footer hidden
- Amber banner at top

─────────────────────────────────
CONFIRM SAVE MODAL
─────────────────────────────────
Max width: 440px, centred

Content:
- Icon: orange circle with 🔢
- Title: "Lock in this format?"
- Body: "This format will be used for all RFIs in this project. You can edit it until the first RFI is raised, after which it will be permanently locked."
- Preview box: shows generated format string (e.g., MGT / RCC_Slab / 2026 / 1)
- Footer: Cancel (secondary) | Confirm & Save (primary, #FC5027)

Post-save:
- Success toast: "✓ RFI numbering format saved successfully."
- Project card switches to Configured state
```

---

## 📣 Release Note Details

**Overview**
digiQC now supports a configurable RFI auto-numbering system. Every RFI raised in a project can carry a unique, structured identifier built from up to 7 levels — such as project code, checklist name, year, and sequence number. This ensures every RFI is traceable and consistently referenced across Web, Mobile, and PDF reports.

**Who Benefits and How**
- **Super Admin (digiQC):** Controls which organisations can use RFI Auto-Numbering via the Addon Services panel — one toggle, full org-level governance
- **System Admin:** Can configure a meaningful RFI number format at any time before the first RFI is raised — accessible directly from project settings whenever RFI is ON
- **Project Manager / Quality Head:** Can view the configured format and reference any RFI by its unique number in reports, dashboards, and audits
- **Site Engineer / QC Inspector:** Sees the RFI number immediately on the mobile screen after raising an RFI — no manual tracking needed
- **Auditors / Clients:** Every RFI in every PDF report carries the same structured identifier, making audits clean and traceable

**What's New**
- RFI Auto-Numbering toggle in Super Admin org settings (requires RFI to be enabled first)
- 7-level format configurator with 13 selectable options including project code, checklist name, year, date, time, reference number, nomenclature levels, and auto-increment number
- Configurator only visible on project settings when RFI is turned ON for the project
- Live preview of the generated RFI number while configuring
- Configurable number start value
- Format locks permanently after the first RFI is raised — editable until then
- RFI number visible on Web (RFI detail, EQC list), Mobile (inspection screens), and all PDF report types
- Rejected RFIs retain their original number; reinspections get a new incremental number

**How It Works**
A Super Admin enables RFI Auto-Numbering for the organisation in Addon Services. A System Admin then opens the project settings, turns RFI ON, and the RFI Numbering Format section appears. The System Admin selects up to 7 levels and sees a live preview of the generated format. Once saved, the format is active for all RFIs in that project. From the moment the first RFI is raised, the format is permanently locked and every subsequent RFI receives the next sequential number in the configured format.
