# Create Bug Test Cases

## TC-CREATE-001 - Create bug with valid data

### Preconditions

* User is logged in.
* User is on the dashboard.

### Test Steps

1. Click on the "+ Add Bug" button.
2. Fill in all required fields with valid data.
3. Click on "Save Bug".

### Expected Result

* The new bug is created successfully.
* A toast message is displayed.
* The new bug appears on the dashboard.

### Status

Not Executed

---

## TC-CREATE-002 - Create bug with empty required fields

### Preconditions

* User is logged in.
* User is on the Create Bug modal.

### Test Steps

1. Leave one or more required fields empty.
2. Click on "Save Bug".

### Expected Result

* The bug is not created.
* Validation messages are displayed.
* The user remains on the Create Bug modal.

### Status

Not Executed

---

## TC-CREATE-003 - Create duplicated bug name

### Preconditions

* User is logged in.
* A bug with the same name already exists.

### Test Steps

1. Click on the "+ Add Bug" button.
2. Enter an existing bug name.
3. Fill in the remaining fields.
4. Click on "Save Bug".

### Expected Result

* The bug is not created.
* A duplicated bug name error message is displayed.

### Status

Not Executed

---

## TC-CREATE-004 - Create bug with maximum field length

### Preconditions

* User is logged in.
* User is on the Create Bug modal.

### Test Steps

1. Enter values near the maximum accepted length for all text fields.
2. Click on "Save Bug".

### Expected Result

* The bug is created successfully.
* No layout issues occur.
* The information is displayed correctly.

### Status

Not Executed

---

## TC-CREATE-005 - Create bug with special characters

### Preconditions

* User is logged in.
* User is on the Create Bug modal.

### Test Steps

1. Enter special characters in the bug name and description.
2. Click on "Save Bug".

### Expected Result

* The bug is created successfully.
* Special characters are displayed correctly.
* No application errors occur.

### Status

Not Executed

---

## TC-CREATE-006 - Create bug with minimum required data

### Preconditions

* User is logged in.
* User is on the Create Bug modal.

### Test Steps

1. Fill only the mandatory fields.
2. Leave optional fields empty.
3. Click on "Save Bug".

### Expected Result

* The bug is created successfully.
* Optional fields remain empty.
* No validation errors occur.

### Status

Not Executed

---

## TC-CREATE-007 - Verify created bug after page refresh

### Preconditions

* User is logged in.

### Test Steps

1. Create a new bug.
2. Refresh the browser page.
3. Return to the dashboard.

### Expected Result

* The bug remains visible.
* All entered information is preserved.
* The data is loaded correctly from localStorage.

### Status

Not Executed
