# Product Requirements Document (PRD) - TODO App Upgrade (MVP + Post-MVP)

## 1. Overview

The current TODO app supports only a task title and completed status. This upgrade introduces lightweight task planning features while keeping the product simple and teachable. The MVP focuses on adding due dates, priority levels, and date-based filters with local-only storage and no backend changes. Additional usability improvements such as overdue highlighting and advanced sorting are explicitly deferred to Post-MVP.

---

## 2. MVP Scope

- Add optional `dueDate` to each task using ISO format `YYYY-MM-DD`.
- Add `priority` to each task with enum values `P1 | P2 | P3`.
- Set default `priority` to `P3` when not provided.
- Add filters/tabs: `All`, `Today`, `Overdue`.
- Keep data storage local only (no backend changes, no external storage).
- Validation and data handling:
  - `title` is required.
  - `dueDate` is optional.
  - Invalid `dueDate` values are ignored and treated as absent.
  - `priority` accepts only `P1`, `P2`, or `P3`.

---

## 3. Post-MVP Scope

- Visually highlight overdue tasks.
- Add sorting behavior:
  - Overdue tasks first.
  - Then by priority (`P1` before `P2` before `P3`).
  - Then by due date ascending.
  - Tasks without a due date last.

---

## 4. Out of Scope

- Notifications.
- Recurring tasks.
- Multi-user support.
- Keyboard navigation and additional accessibility enhancements.
- External storage integrations.
