# Update Bug Test Cases

## TC-UPDATE-001 - Update bug with valid data

### Preconditions

* User is logged in.
* User is on the dashboard.
* At least one bug exists.

### Test Steps

1. Click on "View Details" for an existing bug.
2. Click on "Edit Bug".
3. Update the bug name, family, severity, priority, status and description.
4. Click on "Save Changes".

### Expected Result

* The bug is updated successfully.
* A toast message is displayed.
* The updated information is visible in the bug details modal.
* The updated information is reflected on the dashboard.

### Status

Not Executed

---

## TC-UPDATE-002 - Update bug severity

### Preconditions

* User is logged in.
* User is on the dashboard.
* At least one bug exists.

### Test Steps

1. Click on "View Details" for an existing bug.
2. Click on "Edit Bug".
3. Change the severity value.
4. Click on "Save Changes".

### Expected Result

* The severity is updated successfully.
* The severity badge displays the new value.
* A toast message is displayed.

### Status

Not Executed

---

## TC-UPDATE-003 - Update bug status

### Preconditions

* User is logged in.
* User is on the dashboard.
* At least one bug exists.

### Test Steps

1. Click on "View Details" for an existing bug.
2. Click on "Edit Bug".
3. Change the status value.
4. Click on "Save Changes".

### Expected Result

* The status is updated successfully.
* The status badge displays the new value.
* A toast message is displayed.

### Status

Not Executed

---

## TC-UPDATE-004 - Update bug description only

### Preconditions

* User is logged in.
* User is on the dashboard.
* At least one bug exists.

### Test Steps

1. Click on "View Details" for an existing bug.
2. Click on "Edit Bug".
3. Change only the description field.
4. Click on "Save Changes".

### Expected Result

* The bug description is updated successfully.
* Other bug fields remain unchanged.
* A toast message is displayed.

### Status

Not Executed

---

## TC-UPDATE-005 - Cancel bug update

### Preconditions

* User is logged in.
* User is on the dashboard.
* At least one bug exists.

### Test Steps

1. Click on "View Details" for an existing bug.
2. Click on "Edit Bug".
3. Change one or more fields.
4. Click on "Cancel".

### Expected Result

* Edit mode is closed.
* No changes are saved.
* The original bug information remains unchanged.

### Status

Not Executed

---

## TC-UPDATE-006 - Update bug with empty required field

### Preconditions

* User is logged in.
* User is on the dashboard.
* At least one bug exists.

### Test Steps

1. Click on "View Details" for an existing bug.
2. Click on "Edit Bug".
3. Clear a required field, such as bug name or description.
4. Click on "Save Changes".

### Expected Result

* The bug is not updated.
* A validation message is displayed.
* The user remains in edit mode.

### Status

Not Executed

---

## TC-UPDATE-007 - Verify updated bug after page refresh

### Preconditions

* User is logged in.
* At least one bug exists.

### Test Steps

1. Update an existing bug.
2. Save the changes.
3. Refresh the browser page.
4. Return to the dashboard.
5. Open the updated bug details.

### Expected Result

* The updated information remains visible.
* The changes are loaded correctly from localStorage.

### Status

Not Executed
