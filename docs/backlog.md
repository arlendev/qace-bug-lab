# QAce Bug Lab Backlog

This document contains improvements, future features and technical enhancements identified during development and testing activities.

---

# 🔵 UI Improvements

## UI-001 - Dashboard Header Alignment

### Description

When filters return only one or two bug cards, the visual balance between the dashboard area and action buttons changes slightly.

### Status

Backlog

### Priority

Low

### Notes

Current behavior is acceptable and does not impact usability.

Review after responsive design implementation.

---

## UI-002 - Mobile Header Layout on Small Screens

### Description

On small mobile devices (e.g. iPhone 13 Mini), the Logout button competes for space with dashboard actions, creating visual crowding.

### Environment

- Device: iPhone 13 Mini
- Browser: Safari
- Screen width: 375px

### Current Behavior

- Header elements become visually compressed.
- Filter buttons wrap to multiple lines.
- Visual balance is reduced.

### Expected Behavior

- Improve spacing between dashboard elements.
- Adapt header layout for narrow screens.
- Keep filter buttons centered and visually balanced.

### Status

Backlog

### Priority

Low

### Notes

Application remains fully functional.

Issue affects visual presentation only.

Review during responsive design improvements.

---

## UI-003 - Modal Overflow on Smaller Screens

### Description

When the Edit Bug modal becomes taller than the available viewport height, users may lose access to important actions located at the bottom of the modal.

### Environment

- Dell 15" laptop
- Smaller viewport heights
- Bug Edit Mode

### Current Behavior

- Modal content exceeds viewport height.
- Save Changes and Cancel buttons may become inaccessible.
- Users cannot easily scroll to the bottom of the modal.

### Expected Behavior

- Modal should remain fully accessible on all screen sizes.
- Vertical scrolling should be available when content exceeds viewport height.
- Save Changes and Cancel buttons must always remain reachable.

### Status

Open

### Priority

High

### Notes

Issue discovered during exploratory testing after Sprint 8.

Recommended to resolve before implementing Delete Bug functionality, since future confirmation dialogs will also depend on modal responsiveness.

---

# 🔵 Future Features

## LAB-001 - Bug Simulation Mode

### Description

Introduce a training mode that allows users to intentionally activate predefined application defects.

The objective is to create a realistic QA learning environment where testers can identify, reproduce, document and validate software bugs.

### Proposed Functionality

Users may enable one or more simulated defects through a dedicated interface.

Examples:

- Disable required field validation
- Return incorrect filter results
- Display inconsistent bug details
- Simulate save operation failures
- Introduce UI inconsistencies
- Generate incorrect status updates

### Expected Benefits

- QA practice environment
- Bug reporting exercises
- Test case execution training
- Regression testing scenarios
- Educational demonstrations

### Status

Future Vision

### Priority

Low

### Notes

This feature is intentionally planned for a future phase of the project.

Current focus remains on building a stable and fully tested CRUD application before introducing simulated defects and training scenarios.

---

# 🔵 Technical Improvements

No items registered yet.

---

# 🔵 Roadmap Status

### Sprint 6 - Create Bug

✅ Completed

### Sprint 7 - Local Persistence

✅ Completed

### Sprint 8 - Update Bug

✅ Completed

### Sprint 8.1 - Modal Responsiveness Hotfix

⏳ Planned

### Sprint 9 - Delete Bug

⏳ Planned
