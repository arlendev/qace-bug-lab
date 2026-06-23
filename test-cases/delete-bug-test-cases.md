# Delete Bug Test Cases

## TC-DELETE-001 - Delete an existing bug

### Preconditions

- User is logged in.
- User is on the dashboard.
- At least one bug exists.

### Test Steps

1. Click on "View Details" for an existing bug.
2. Click on "Delete Bug".
3. Click on "Delete" in the confirmation dialog.

### Expected Result

- The bug is deleted successfully.
- The bug no longer appears on the dashboard.
- A toast message is displayed.

### Status

Not Executed

---

## TC-DELETE-002 - Cancel bug deletion

### Preconditions

- User is logged in.
- User is on the dashboard.
- At least one bug exists.

### Test Steps

1. Click on "View Details" for an existing bug.
2. Click on "Delete Bug".
3. Click on "Cancel".

### Expected Result

- The confirmation dialog closes.
- The bug remains unchanged.
- No deletion occurs.

### Status

Not Executed

---

## TC-DELETE-003 - Delete bug with active filter

### Preconditions

- User is logged in.
- A severity filter is active.
- At least one bug matching the filter exists.

### Test Steps

1. Apply a severity filter.
2. Open a bug matching the filter.
3. Delete the bug.

### Expected Result

- The bug is deleted successfully.
- The filter remains active.
- Remaining bugs continue to be displayed correctly.

### Status

Not Executed
