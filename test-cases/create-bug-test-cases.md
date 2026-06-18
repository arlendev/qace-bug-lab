# Create Bug Test Cases

## TC-CREATE-001 - Create bug with valid data

### Preconditions

- User is logged in.
- User is on the dashboard.

### Test Steps

1. Click on the "+ Add Bug" button.
2. Fill in all required fields with valid data.
3. Click on "Save Bug".

### Expected Result

- The new bug is created successfully.
- A toast message is displayed.
- The new bug appears on the dashboard.

### Status

Not Executed

---

## TC-CREATE-002 - Create bug with empty required fields

### Preconditions

- User is logged in.
- User is on the Create Bug modal.

### Test Steps

1. Leave one or more required fields empty.
2. Click on "Save Bug".

### Expected Result

- The bug is not created.
- An error message is displayed.

### Status

Not Executed

---

## TC-CREATE-003 - Create duplicated bug name

### Preconditions

- User is logged in.
- A bug with the same name already exists.

### Test Steps

1. Click on the "+ Add Bug" button.
2. Enter an existing bug name.
3. Fill in the remaining fields.
4. Click on "Save Bug".

### Expected Result

- The bug is not created.
- A duplicated bug name error message is displayed.

### Status

Not Executed
