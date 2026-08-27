# Product Requirements Document (PRD) - Todo App Upgrade

## 1. Overview

We are upgrading the basic Todo app to support due dates, task priorities, and filter views so users can better organize and prioritize work without adding complexity. The goal is to keep the product simple and teachable while making task management more practical for daily use.

The MVP focuses on adding the core functionality requested by stakeholders: optional due dates, priority levels, and quick filtering of tasks by date status. Post-MVP items are limited to visual overdue emphasis and sorting improvements. The app will remain local-only and will not introduce backend or multi-user features.

---

## 2. MVP Scope

- Add an optional `dueDate` field to each task using ISO format `YYYY-MM-DD`
- Add a `priority` field with the allowed values `P1`, `P2`, and `P3`
- Default `priority` to `P3` when not explicitly set
- Keep task storage local to the browser/app instance; no backend or external storage integration
- Provide task filtering tabs for:
  - All
  - Today
  - Overdue
- In the `All` view, show both incomplete and completed tasks
- In the `Today` and `Overdue` views, show only incomplete tasks
- Allow users to set and display task due dates in a lightweight, easy-to-understand format
- Add visual priority badges or labels using the requested color scheme:
  - `P1`: red
  - `P2`: orange
  - `P3`: gray
- Validate task data such that:
  - `title` is required
  - `priority` must be one of `P1`, `P2`, or `P3`
  - invalid `dueDate` values are ignored and treated as absent
- Keep the product lean and simple, with no advanced accessibility or keyboard navigation requirements for MVP

---

## 3. Post-MVP Scope

- Add visual highlighting for overdue tasks so they stand out clearly in the list
- Implement sorting in the following order:
  1. overdue tasks first
  2. then by priority (`P1` to `P3`)
  3. then by due date ascending
  4. then tasks without a due date last
- Refine the task list presentation to make urgency and prioritization easier to scan at a glance
- Continue to maintain the local-only architecture without introducing backend complexity

---

## 4. Out of Scope

- Notifications or reminders for task due dates
- Recurring tasks
- Multi-user support
- Keyboard navigation or specialized accessibility enhancements beyond basic usability
- External storage or backend persistence
- Advanced workflow features beyond the requested due dates, priorities, and filters
