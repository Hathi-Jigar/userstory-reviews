# User Story Reviews

Review space for digiQC user stories. Every user story and its interactive HTML prototype starts here for review before being moved to the `product-management` repo.

## Flow

```
1. Author writes user story (.md) + interactive prototype (.html) in Claude
2. Claude pushes both to this repo → review page auto-generated
3. Author shares review link with senior
4. Senior opens link → selects text → comments inline
5. Author edits directly on the review page → resolves comments
6. Senior approves (or author decides to move)
7. Author clicks "Move" button on review page → selects folder in product-management → story moves
8. Prototype is separately pushed to product-management/docs/screens/<us-name>/ for GitHub Pages
```

## What Goes Where

| File | This Repo (userstory-reviews) | Main Repo (product-management) |
|------|-------------------------------|-------------------------------|
| User story `.md` | `reviews/<us-name>/spec.md` | Moved via Move button → `Roadmap/<epic>/US-xxx.md` |
| Prototype `.html` | `reviews/<us-name>/prototype.html` | `docs/screens/<us-name>/index.html` (GitHub Pages) |
| Review page | `reviews/<us-name>/index.html` | — (stays here) |
| Comments | `reviews/<us-name>/comments.json` | — (stays here) |
| Decision | `reviews/<us-name>/decision.json` | — (stays here) |

## Stories

| # | User Story | Status | Review Link |
|---|-----------|--------|-------------|
| 1 | Instruction: Role-Based Action Control & Team-Scoped Visibility | Under Review | [Open Review](https://hathi-jigar.github.io/userstory-reviews/reviews/us-instruction-rbac/) |
| 2 | Issue Assignment with Assignee & Notification Recipients | Under Review | [Open Review](https://hathi-jigar.github.io/userstory-reviews/reviews/us-issue-assignment-notification/) |
| 3 | RFI Auto-Numbering with 7-Level Configurator | Under Review | [Open Review](https://hathi-jigar.github.io/userstory-reviews/reviews/us-rfi-auto-numbering/) |

## Dashboard

View all stories with live status, comments, reviewer, and copy-paste links:

**[Open Dashboard](https://hathi-jigar.github.io/userstory-reviews/)**

## Review Page Features

- **Inline commenting** — select text → add comment
- **Edit mode** — author edits the spec directly on the review page
- **Approve / Changes Needed** — senior sets review status
- **Move button** — moves approved story to product-management repo (select destination folder)
- **Live prototype** — embedded iframe of the interactive HTML prototype

## How to Review (for Senior)

1. Open the review link shared with you
2. First visit: enter your name + access key (saved in browser, one-time)
3. Select any text in the spec → comment popup appears → type your feedback → Submit
4. Click **Approve** when satisfied, or **Changes Needed** if changes are required
