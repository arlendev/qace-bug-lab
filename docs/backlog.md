# QAce Bug Lab Backlog

This document contains improvements, future features and technical enhancements identified during development and testing activities.

---

## UI Improvements

### UI-001 - Dashboard Header Alignment

**Description:**

When filters return only one or two bug cards, the visual balance between the "Bug Dashboard" title and the Logout button changes slightly.

**Status:**

Backlog

**Priority:**

Low

**Notes:**

Current behavior is acceptable and does not impact usability.
Review after responsive design implementation.

---

### UI-002 - Mobile Header Layout on Small Screens

**Description:**

On small mobile devices (e.g. iPhone 13 Mini), the Logout button competes for space with the "Bug Dashboard" title, creating visual crowding.

**Environment:**

- Device: iPhone 13 Mini
- Browser: Safari
- Screen width: 375px

**Current Behavior:**

The Logout button remains aligned on the same row as the dashboard title.
Severity filter buttons wrap to multiple lines, reducing visual balance.

**Expected Behavior:**

- Improve spacing between title and Logout button.
- Adapt header layout for narrow screens.
- Keep filter buttons centered and visually balanced.

**Status:**

Backlog

**Priority:**

Low

**Notes:**

Application remains fully functional.
Issue affects visual presentation only.
Review during responsive design improvements.

---

## Future Features

### LAB-001 - Bug Simulation Mode

**Description:**

Introduce a training mode that allows users to intentionally activate predefined application defects.

The objective is to create a realistic QA learning environment where testers can identify, reproduce, document and validate software bugs.

**Proposed Functionality:**

Users may enable one or more simulated defects through a dedicated interface.

Examples:

- Disable required field validation
- Return incorrect filter results
- Display inconsistent bug details
- Simulate save operation failures
- Introduce UI inconsistencies
- Generate incorrect status updates

**Expected Benefits:**

- QA practice environment
- Bug reporting exercises
- Test case execution training
- Regression testing scenarios
- Educational demonstrations

**Status:**

Future Vision

**Priority:**

Low

**Notes:**

This feature is intentionally planned for a future phase of the project.

Current focus remains on building a stable and fully tested CRUD application before introducing simulated defects and training scenarios.

---

## Technical Improvements

No items registered yet.
