# MVP

- Epic: Task Due Dates
  - Story: Add optional due date field to tasks
    - Acceptance Criteria: A task can be created without a due date
    - Acceptance Criteria: A task can store a due date in `YYYY-MM-DD` format
    - Technical Requirements: Add an optional `dueDate` task property and accept ISO `YYYY-MM-DD` values
  - Story: Display task due dates
    - Acceptance Criteria: A task's due date is displayed in a lightweight, understandable format when present
    - Acceptance Criteria: No due date is displayed when a task has no due date
    - Technical Requirements: Render the due date only when `dueDate` is present and format it for readable display
  - Story: Validate task due date values
    - Acceptance Criteria: An invalid due date is ignored and treated as absent
    - Technical Requirements: Validate `dueDate` values before storing or rendering them and normalize invalid values to absent

- Epic: Task Priorities
  - Story: Add priority field to tasks
    - Acceptance Criteria: A task supports the priority values `P1`, `P2`, and `P3`
    - Technical Requirements: Add a `priority` task property constrained to the values `P1`, `P2`, and `P3`
  - Story: Default task priority to P3
    - Acceptance Criteria: A task defaults to `P3` when no priority is provided
    - Technical Requirements: Apply `P3` during task creation or task-data normalization when `priority` is missing
  - Story: Validate task priority values
    - Acceptance Criteria: Values outside `P1`, `P2`, and `P3` are rejected or treated as invalid task data
    - Technical Requirements: Validate priorities against an explicit allowed-value list before accepting task data
  - Story: Display color-coded priority badges
    - Acceptance Criteria: `P1` is displayed with a red badge or label
    - Acceptance Criteria: `P2` is displayed with an orange badge or label
    - Acceptance Criteria: `P3` is displayed with a gray badge or label
    - Technical Requirements: Map each allowed priority to a distinct badge or label style using red for `P1`, orange for `P2`, and gray for `P3`

- Epic: Task Data Validation
  - Story: Require task titles
    - Acceptance Criteria: A task cannot be created without a title
    - Technical Requirements: Reject task creation when `title` is missing or empty

- Epic: Task Filtering
  - Story: Add All tasks filter tab
    - Acceptance Criteria: Selecting All displays both incomplete and completed tasks
    - Technical Requirements: Add an All filter state that returns tasks without filtering by completion status
  - Story: Add Today tasks filter tab
    - Acceptance Criteria: Selecting Today displays incomplete tasks due today
    - Technical Requirements: Compare valid `dueDate` values with the current local calendar date and exclude completed tasks
  - Story: Add Overdue tasks filter tab
    - Acceptance Criteria: Selecting Overdue displays incomplete tasks whose due dates have passed
    - Technical Requirements: Compare valid `dueDate` values with the current local calendar date and return only past-due incomplete tasks
  - Story: Show completed tasks in the All view
    - Acceptance Criteria: Completed tasks are included when the All view is selected
    - Technical Requirements: Preserve completed tasks in the source collection and include them in the All view result
  - Story: Show only incomplete tasks in Today and Overdue views
    - Acceptance Criteria: Completed tasks are excluded from the Today view
    - Acceptance Criteria: Completed tasks are excluded from the Overdue view
    - Technical Requirements: Apply the incomplete-task condition to both the Today and Overdue filter predicates

- Epic: Local Task Storage
  - Story: Store task data locally
    - Acceptance Criteria: Task data remains available within the same browser/app instance
    - Technical Requirements: Keep task state in the existing client-side storage mechanism and preserve due dates and priorities with each task
  - Story: Keep task storage free of backend integration
    - Acceptance Criteria: The MVP does not require a backend or external storage service
    - Technical Requirements: Do not add API calls, server persistence, or external storage dependencies for task data

# Post-MVP

- Epic: Overdue Task Visibility
  - Story: Highlight overdue tasks in the task list
    - Acceptance Criteria: Incomplete overdue tasks have a visual treatment that distinguishes them from other tasks
    - Technical Requirements: Derive overdue status from an incomplete task's valid `dueDate` being earlier than the current local date and apply a distinct visual style

- Epic: Task Sorting
  - Story: Sort overdue tasks first
    - Acceptance Criteria: Overdue tasks appear before non-overdue tasks
    - Technical Requirements: Use overdue status as the first comparator in the task-list sort
  - Story: Sort tasks by priority
    - Acceptance Criteria: Within the sorting order, tasks are ordered from `P1` to `P3`
    - Technical Requirements: Use an explicit priority ranking of `P1`, `P2`, then `P3` as the second comparator
  - Story: Sort tasks by ascending due date
    - Acceptance Criteria: Tasks with due dates are ordered from earliest to latest when earlier sorting criteria are equal
    - Technical Requirements: Compare valid due dates chronologically as the third comparator
  - Story: Place tasks without due dates last
    - Acceptance Criteria: Tasks without due dates appear after tasks with due dates when earlier sorting criteria are equal
    - Technical Requirements: Treat absent or invalid due dates as greater than valid due dates in the final due-date comparator
  - Story: Refine task list scanability
    - Acceptance Criteria: Task list presentation makes urgency and prioritization easier to scan at a glance
    - Technical Requirements: Present overdue status, due dates, and priority indicators consistently in each task row without changing the local-only task model
