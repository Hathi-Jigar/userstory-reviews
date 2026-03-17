# Feature PRD — Instruction: Role-Based Action Control & Team-Scoped Visibility

**Module / Area:** Instructions (Mobile App)

**Type:** Enhancement

**Interactive Prototype:**
- [View Live Screen](https://digiqc-hq.github.io/product-management/screens/us-instruction-rbac/)
- [View Source Code](https://github.com/digiqc-hq/product-management/blob/main/docs/screens/us-instruction-rbac/index.html)

---

## 📌 Brief Description

Today, any member of any involved team can see all instructions on a project, and action controls like respond, close, accept, and reject are not clearly gated by role or team membership. This creates confusion on-site — users see instructions that don't involve them, and sensitive actions can be taken by the wrong people.

This enhancement tightens who can see an instruction and who can take each action on it. Only teams directly involved in an instruction (raising team or assigned team) can view it. Actions like Close, Respond, Accept, and Reject are restricted to the right team and the right users within that team. For users who belong to multiple teams, a team-picker is shown at raise time so the instruction is always attributed to the correct team.

---

## 🎯 Jobs to Be Done (JTD)

| Role | When… | They want to… | So they can… |
|------|--------|---------------|--------------|
| Site Engineer (Raising Right) | Raising an instruction from a project where they are in multiple teams | Select which team they are raising from | Ensure the instruction is linked to the correct team and the right people are notified |
| Site Engineer (Raising Right) | After an assigned team has responded | Accept or reject the response | Confirm the corrective action is satisfactory or push it back |
| Site Engineer (Raising Right) | When an issue is resolved directly without needing a response | Close the instruction from their side | Avoid unnecessary back-and-forth when the fix is obvious |
| Site Engineer (Assigned Team) | Receiving an instruction about their work | Respond to the instruction with remarks or evidence | Show that corrective action has been taken |
| Project Manager / QC Head | Reviewing open instructions | See only instructions relevant to their team | Stay focused without being overwhelmed by unrelated issues |

---

## 💡 How Might We (HMW)

- How might we ensure that users only see instructions where their team is directly involved, without hiding data they legitimately need?
- How might we make it clear to an assigned team member that they can respond but cannot close or accept?
- How might we handle the team-selection step at raise time gracefully, so it only appears when it is actually needed (multi-team users)?
- How might we make the raising user's accept/reject authority clear in the UI without adding friction for straightforward cases?
- How might we ensure that the To Do tab always shows only the actions a user is genuinely responsible for taking?

---

## 🤖 User Persona

| Role | Context of Use | Goal | Frustration | Success |
|------|----------------|------|-------------|---------|
| Site Engineer (Raising Right) | On-site, mobile, raising an instruction mid-inspection | Raise and close instructions quickly | Sees instructions from other teams they don't manage — cluttered To Do tab | To Do tab shows only what they need to act on; actions are clear |
| Site Engineer (Assigned Team) | On-site, mobile, checking what needs to be fixed | Respond to instructions assigned to their team | Cannot tell if they are expected to respond or just informed | A clear Respond button is visible only when it is their turn to act |
| Project Manager / QC Head | Office or site review, checking instruction health | Get a focused view of team-level instruction status | Sees all instructions across all teams — hard to filter what matters | Instruction list is scoped to their team involvement |

---

## 📖 User Story

> As a **Site Engineer with raising rights**, I want instruction visibility and actions to be controlled by team involvement, so that only the right people see and act on each instruction at each stage.

> As a **Site Engineer in an assigned team**, I want to see and respond to instructions assigned to my team, so that I can take corrective action without accessing instructions that don't involve me.

> As a **user who belongs to multiple teams**, I want to be asked which team I am raising from when I raise an instruction, so that the instruction is correctly attributed and the right team members are involved.

---

## ✅ Acceptance Criteria

### Instruction Visibility — Who Can See an Instruction

- [ ] All three tabs — **To Do, Raised, and Draft** — are visible to every project member with an **Inspector** or **Project Admin** role
- [ ] Tab visibility is the same for everyone on the project — the tabs are never hidden based on role or rights
- [ ] Across all tabs, a specific instruction is only shown to a user if they are part of the **raising team** or the **assigned team** for that instruction
- [ ] Users who are not part of the raising team or assigned team for an instruction cannot see that instruction in any tab
- [ ] If a user belongs to both the raising team and the assigned team for the same instruction, they act based on raising rights (raising rights take priority over assigned team membership)

---

### Tab Behaviour — To Do, Raised, Draft

- [ ] **To Do tab** is visible to all project members (Inspector / Project Admin). Data shown:
  - User with raising rights (raising team): instructions in **Responded** status where Accept/Reject is pending, for instructions raised by their team
  - Assigned team user: instructions in **Raised** or **Rejected** status where their team's response is pending
  - Only instructions where the user is part of the raising team or assigned team are shown
  - User with no involvement in any instruction: tab is visible but empty
- [ ] **Raised tab** is visible to all project members (Inspector / Project Admin). Data shown:
  - User **with Raise Instruction rights**: instructions raised by their own team only, that are yet to be responded to (status = Raised)
  - User **without Raise Instruction rights**: tab is visible but always empty — no data is shown regardless of team membership
- [ ] **Draft tab** is visible to all project members (Inspector / Project Admin). Data shown:
  - Instructions saved as drafts by the current user only — not shared with the team
  - Users who have never saved a draft see an empty tab
- [ ] Empty state messages per tab:
  - To Do (no pending actions): "No pending actions. You're all caught up."
  - To Do (not part of any raising or assigned team): "No instructions are assigned to you or your team yet."
  - Raised tab (user with rights, no unresponded instructions from their team): "No open instructions. All raised instructions have been responded to."
  - Raised tab (user without Raise Instruction rights): "You don't have permission to raise instructions on this project."
  - Draft tab (no drafts saved): "No drafts saved. Instructions you pause mid-way will appear here."

---

### Raising an Instruction — Team Selection

- [ ] When a user who belongs to **only one team** raises an instruction, no team-selection step is shown — the instruction is automatically attributed to their single team
- [ ] When a user who belongs to **multiple teams** raises an instruction, a **"Raise from which team?"** picker is shown before they proceed
- [ ] The team picker shows only the teams the user belongs to for that project
- [ ] The user must select a team before they can continue — the picker cannot be skipped
- [ ] The selected team is shown on the instruction detail screen as the "Raising Team"

---

### Close — Raising Team Action

- [ ] Any member of the **raising team who has raising rights** can close an instruction directly — but only when no response has been submitted
- [ ] Direct close is available when the instruction is in **Raised** status (no response yet) or **Rejected** status (response was rejected and no new response has been submitted)
- [ ] Once the assigned team submits a response (status = Responded), the Close button is no longer available — the raising team must Accept or Reject the response instead
- [ ] Members of the raising team **without** raising rights cannot close the instruction
- [ ] Members of the assigned team cannot close the instruction
- [ ] When a raising team user taps Close, a confirmation prompt is shown: "Close this instruction? No response has been submitted. This will mark it as resolved."
- [ ] After close, the instruction moves to **Closed** status and is removed from To Do for both teams
- [ ] A remark field is shown on the close confirmation — optional, but available

---

### Respond — Assigned Team Action

- [ ] Any member of the **assigned team** can submit a response to an instruction
- [ ] The Respond action is only available when the instruction is in **Raised** or **Rejected** status
- [ ] Members of the raising team cannot respond to their own instruction
- [ ] The response must include at minimum a text remark; attaching a photo is optional
- [ ] After response is submitted, the instruction moves to **Responded** status
- [ ] The instruction appears in the raising team user's (with raising rights) To Do tab as pending Accept/Reject

---

### Accept / Reject — Raising Team Action

- [ ] Only members of the **raising team who have raising rights** can Accept or Reject a response
- [ ] Accept and Reject actions are only available when the instruction is in **Responded** status
- [ ] Members of the raising team without raising rights cannot Accept or Reject — they have no action buttons on this screen
- [ ] Members of the assigned team cannot Accept or Reject
- [ ] When a raising team user taps Accept, a confirmation prompt is shown: "Accept this response? The instruction will be marked as Closed."
- [ ] After Accept, the instruction moves to **Closed** status — accepting a response is equivalent to closing the instruction
- [ ] When a raising team user taps Reject, a remark field is required — they must explain what is insufficient before rejecting
- [ ] After Reject, the instruction moves to **Rejected** status and the assigned team is notified to respond again
- [ ] Reject reason is shown prominently in the instruction detail for the assigned team

---

### Raising Rights — Who Has Them & What They Control

- [ ] Raising rights are configured per user per project in the project settings
- [ ] A user without raising rights can see all three tabs — but the Raised tab will always be empty for them
- [ ] A user without raising rights cannot raise, close, accept, or reject — they can only respond when their team is assigned
- [ ] Raising rights determine who can: raise a new instruction, see data in the Raised tab, close an instruction (pre-response), accept a response, reject a response
- [ ] If a user with raising rights is removed from the raising team mid-instruction, they lose all raising team privileges on that instruction going forward

---

### Role & Permission Summary

| Action | Who Can Do It | When Available |
|--------|---------------|----------------|
| See tabs (To Do / Raised / Draft) | All project members (Inspector / Project Admin) | Always — tabs always visible |
| See data in Raised tab | Users with Raise Instruction rights, for their own team's instructions only | Tab is visible to all; data scoped to user's team and rights |
| Raise Instruction | Users with Raise Instruction rights | Always |
| Close (Direct) | Users with Raise Instruction rights | Status = Raised or Rejected (no pending response) |
| Respond | Assigned team members | Status = Raised or Rejected |
| Accept Response | Users with Raise Instruction rights | Status = Responded |
| Reject Response | Users with Raise Instruction rights | Status = Responded |

---

### States & Validations

- [ ] If a user tries to perform an action they don't have rights to, the action button is not shown — it is not just disabled, it is hidden
- [ ] If the Close action is tapped without any remark, it still proceeds — remark is optional for close
- [ ] If the Reject action is tapped without a remark, submission is blocked — remark is required for reject
- [ ] Empty state messages per tab and role:
  - To Do (no pending actions): "No pending actions. You're all caught up."
  - To Do (not part of any raising or assigned team): "No instructions are assigned to you or your team yet."
  - Raised tab (user with rights, no unresponded instructions from their team): "No open instructions. All raised instructions have been responded to."
  - Raised tab (user without Raise Instruction rights): "You don't have permission to raise instructions on this project."
  - Draft tab (no drafts): "No drafts saved. Instructions you pause mid-way will appear here."

---

### Flow Continuity — What Happens Next

- [ ] After an instruction is raised — assigned team members see it in their To Do tab
- [ ] After a response is submitted — raising team user (with raising rights) sees it in their To Do tab for Accept/Reject
- [ ] After Accept — both teams see the instruction as Closed; it leaves To Do for both
- [ ] After Reject — assigned team sees the instruction return to their To Do tab with the rejection reason visible
- [ ] After Close (direct by raising team) — instruction leaves To Do for both teams; assigned team sees it as Closed in their view

---

### Notifications

- [ ] When an instruction is raised and assigned to a team — all members of the assigned team receive a push notification
- [ ] When a response is submitted — all members of the raising team with raising rights receive a push notification
- [ ] When a response is accepted — all members of the assigned team receive a push notification
- [ ] When a response is rejected — all members of the assigned team receive a push notification with the rejection reason
- [ ] When an instruction is closed directly — all members of the assigned team receive a notification

---

## ⚠️ Edge Cases & Constraints

**Positive Cases**
- [ ] User 1 is in Team A (raising team) and Team D. When they raise from Team A, only Team A members (with raising rights) and the assigned team see this instruction in their To Do — Team D members who are not involved see tabs but no data for this instruction
- [ ] User 1 has raising rights. They raise an instruction and the assigned team responds. User 1 sees it in To Do for Accept/Reject, and the Close button is no longer shown
- [ ] User 6 is in Team C with raising rights. They cannot see instructions raised by User 1 from Team A — different raising team, not involved

**Negative Cases**
- [ ] A user in the assigned team should not see a Close or Accept/Reject button at any point
- [ ] A user **without raising rights** sees all three tabs but the Raised tab is always empty — they cannot raise, close, accept, or reject
- [ ] A user not involved in an instruction (not raising team, not assigned team) sees the tabs but that instruction does not appear in any tab for them
- [ ] Once a response is submitted (status = Responded), the Close button must not appear — raising team must Accept or Reject

**Edge Cases**
- [ ] User 1 is in Team A and Team D. They raise from Team A. Later they are removed from Team A — they should lose raising team rights on that instruction
- [ ] If the assigned team has no members with active accounts, the instruction should still be raiseable — but a warning may be shown: "No active members in the assigned team"
- [ ] If an instruction is in Draft status (paused), the raising team can still edit or discard it; no action is available to the assigned team until it is formally raised
- [ ] If a user is added to the assigned team after an instruction is already raised to that team, they should gain visibility of the instruction from the point they were added
- [ ] An instruction in Rejected status with no new response submitted — Close must still be available to the raising team (with rights), since no pending response exists

**How to Test**
- Test with User 1 (multi-team) raising an instruction — verify team picker appears and the instruction is scoped to the selected team
- Test with User 6 (single team) raising — verify no team picker appears
- Log in as a user WITHOUT raising rights — verify all 3 tabs are visible, Raised tab is empty with the no-permission message, no Close/Accept/Reject buttons on any instruction
- Log in as assigned team member — verify only Respond is available, and only in Raised or Rejected status
- Log in as a user not involved in a specific instruction — verify the 3 tabs are visible but that instruction does not appear in any tab
- Test Reject flow — verify remark is mandatory and the instruction moves to Rejected status; assigned team sees it in To Do again
- Test direct Close in Raised status — verify it closes without requiring a response
- Test direct Close in Responded status — verify Close button is not visible; only Accept/Reject is shown
- Test direct Close in Rejected status (no new response yet) — verify Close is still available

---

## 🎨 Design Prompt

```
Screen: Instruction Module — Role-Based Action Control
Platform: Mobile (Android / iOS)
Audience: Site engineers, QC inspectors, field use
Style: Clean, high contrast, large tap targets. digiQC mobile design system.

Instruction Statuses:
- Raised (orange) — instruction raised, awaiting response
- Responded (blue) — assigned team has submitted a response
- Rejected (red) — raising team rejected the response
- Closed (green) — instruction resolved (either direct close or accepted response)

Screens to show:

1. INSTRUCTION LIST — THREE TABS
   - Tab bar at top: To Do | Raised | Draft
   - All three tabs are always visible to every project member (Inspector / Project Admin role)
   - Each instruction card shows: Title, Assigned Team, Status badge, Raised By, Date
   - Status badge colours: Raised = orange, Responded = blue, Rejected = red, Closed = green
   - To Do tab: shows instructions where the user has a pending action — only for instructions where they are part of the raising team or assigned team
   - Raised tab: shows instructions raised by the user's own team, status = Raised, only if user has Raise Instruction rights — users without rights see empty tab
   - Draft tab: current user's own drafts only
   - Empty states:
     - To Do (no pending actions): "No pending actions. You're all caught up."
     - To Do (not part of any raising or assigned team): "No instructions are assigned to you or your team yet."
     - Raised tab (user with rights, all responded): "No open instructions. All raised instructions have been responded to."
     - Raised tab (user without Raise Instruction rights): "You don't have permission to raise instructions on this project."
     - Draft tab: "No drafts saved. Instructions you pause mid-way will appear here."

2. TEAM PICKER (only for multi-team users on raise)
   - Appears as a bottom sheet before the raise form loads
   - Title: "Raising from which team?"
   - List of the user's teams for that project — tap to select
   - Confirm button at bottom
   - Cannot be dismissed without selecting a team

3. INSTRUCTION DETAIL — RAISING TEAM VIEW (with raising rights)
   - Header: Instruction title, status badge
   - Section: Raising Team | Assigned Team | Raised By | Date
   - Response section (if submitted): shows response text + photo thumbnails + Reject reason if previously rejected
   - Action buttons at bottom — context-sensitive:
     - Status = Raised: [Close] button only
     - Status = Responded: [Accept] and [Reject] buttons only — no Close button
     - Status = Rejected (no new response): [Close] button only
     - Status = Closed: no action buttons — read only
   - Close tapped — confirmation bottom sheet: "Close this instruction? No response has been submitted. This will mark it as resolved." + optional remark field + [Confirm Close] + [Cancel]
   - Accept tapped — confirmation bottom sheet: "Accept this response? The instruction will be marked as Closed." + [Yes, Accept] + [Cancel]
   - Reject tapped — bottom sheet: "Why are you rejecting this response?" + mandatory remark text field + [Confirm Reject] + [Cancel]

4. INSTRUCTION DETAIL — ASSIGNED TEAM VIEW
   - Same header and info section
   - Reject reason shown prominently (highlighted block) if status is Rejected
   - Action button at bottom: [Respond] — only if status is Raised or Rejected
   - No Close, Accept, or Reject buttons visible at all
   - Respond tapped — opens Respond form: remark field (required) + photo attach (optional) + [Submit Response]

5. INSTRUCTION DETAIL — VIEW-ONLY (user without raising rights, not on assigned team)
   - All info visible including status and any responses
   - No action buttons shown at all — read only

States to show:
- Default: instruction detail loaded with correct action buttons per role and status
- Loading: skeleton card rows
- Error: "Unable to load instructions. Please try again." with [Retry] button
- Success (after each action): toast at bottom of screen:
  - After Close: "Instruction closed successfully."
  - After Accept: "Response accepted. Instruction is now closed."
  - After Reject: "Response rejected. Assigned team has been notified."
  - After Respond: "Response submitted successfully."

Pop-ups / Modals with messages:
- Close confirmation: "Close this instruction? No response has been submitted. This will mark it as resolved." + optional remark + [Confirm Close] + [Cancel]
- Accept confirmation: "Accept this response? The instruction will be marked as Closed." + [Yes, Accept] + [Cancel]
- Reject: "Why are you rejecting this response?" + mandatory remark text field + [Confirm Reject] + [Cancel]
- Team picker: bottom sheet, cannot be dismissed without selection

Role-based visibility:
- All project members (Inspector / Project Admin): all 3 tabs always visible
- Data in any tab is shown only if the user is part of the raising team or assigned team for that instruction
- User with Raise Instruction rights: sees data in Raised tab (own team's instructions only, status = Raised); sees Close / Accept+Reject action buttons
- User without Raise Instruction rights: Raised tab visible but always empty; no Close, Accept, or Reject buttons
- Assigned team user: sees Respond only when status is Raised or Rejected
- User not involved in a specific instruction: that instruction does not appear in any tab for them

Navigation / Next Step:
- After raise: goes back to Raised tab, new instruction appears at top
- After respond: goes back to To Do tab; instruction leaves assigned team's To Do
- After accept/close: goes back to To Do tab; instruction removed from raising team's To Do
- After reject: instruction leaves raising team's To Do; assigned team sees it in their To Do again

Notes:
- Keep the action bar at the bottom of the screen — full width, high contrast
- Accept button: green fill. Reject button: outlined red. Close button: outlined grey/neutral.
- Respond button: primary brand colour fill
- Rejection reason must be shown as a highlighted block (e.g., light red background) at the top of the response section — not buried at the bottom
- Never show Close and Accept+Reject on the same screen at the same time
```

---

## 📣 Release Note Details

**Overview**
The Instructions module now controls who can see and act on each instruction based on team involvement and raising rights. Instructions are visible only to members of the raising team or the assigned team. Each action — Close, Respond, Accept, Reject — is available only to the right team, the right user, and at the right status.

**Who Benefits & How**
- **Site Engineers (Raising Rights):** See only their own team's unresponded instructions in the Raised tab. Can close directly when no response exists, or accept/reject once a response is submitted
- **Site Engineers (Assigned Team):** See instructions assigned to their team in To Do and can respond when status is Raised or Rejected
- **All Field Users:** All tabs are always accessible — data inside is scoped to instructions where they are directly involved, keeping the view clean and relevant

**What's New**
- All tabs (To Do, Raised, Draft) are always visible to all project members — data inside is scoped by team involvement and raising rights
- Raised tab shows only the user's own team's instructions (status = Raised), and only for users with Raise Instruction rights
- To Do and Draft tabs show data only for instructions where the user is part of the raising team or assigned team
- Four clear statuses: **Raised → Responded → Rejected → Closed**
- Close is only available before a response exists (Raised or Rejected with no pending response) — once a response is submitted, only Accept or Reject is available
- Respond is only available in Raised or Rejected status
- Users without Raise Instruction rights see the Raised tab as empty and cannot Close, Accept, or Reject
- Multi-team users are prompted to select which team they are raising from before creating an instruction
- Meaningful empty state messages on every tab so users are never left on a blank screen

**How It Works**
When an instruction is raised, it is linked to a raising team and an assigned team. Only members of those two teams see the instruction across all tabs. The Raised tab shows the raising team's own unresponded instructions to users with raising rights. The To Do tab shows each user only what needs their action right now. Direct close is available only when no response is pending — once the assigned team responds, the raising team must Accept or Reject. Accepting a response closes the instruction automatically.

---

**Interactive Prototype:**
- [View Live Screen](https://digiqc-hq.github.io/product-management/screens/us-instruction-rbac/)
- [View Source Code](https://github.com/digiqc-hq/product-management/blob/main/docs/screens/us-instruction-rbac/index.html)
