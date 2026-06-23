# Persistence Test Cases

## TC-PERSIST-001 - Created bug persists after page refresh

### Preconditions

- User is logged in.

### Test Steps

1. Create a new bug.
2. Refresh the browser page.
3. Return to the dashboard.

### Expected Result

- The created bug remains visible.
- The bug data is loaded correctly from localStorage.

### Status

Not Executed

---

## TC-PERSIST-002 - Updated bug persists after page refresh

### Preconditions

- User is logged in.
- At least one bug exists.

### Test Steps

1. Edit an existing bug.
2. Save the changes.
3. Refresh the browser page.

### Expected Result

- The updated information remains visible.
- The changes are loaded correctly from localStorage.

### Status

Not Executed

---

## TC-PERSIST-003 - Deleted bug remains deleted after page refresh

### Preconditions

- User is logged in.
- At least one bug exists.

### Test Steps

1. Delete an existing bug.
2. Refresh the browser page.

### Expected Result

- The deleted bug does not reappear.
- The dashboard reflects the updated data.

### Status

Not Executed

---

## TC-PERSIST-004 - Existing seed bugs load correctly on first execution

### Preconditions

- localStorage is empty.

### Test Steps

1. Clear localStorage.
2. Open the application.

### Expected Result

- The initial bug catalog is loaded.
- Default bug cards are displayed correctly.

### Status

Not Executed
