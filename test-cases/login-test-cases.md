# Login Test Cases

## TC-LOGIN-001 - Login with Empty Fields

### Preconditions

- User is on the Login screen.

### Steps

1. Leave Email empty.
2. Leave Password empty.
3. Click Login.

### Expected Result

The system displays the message:

"Please enter email and password."

### Actual Result

The validation message is displayed.

### Status

PASS

---

## TC-LOGIN-002 - Login with Invalid Credentials

### Preconditions

- User is on the Login screen.

### Steps

1. Enter an invalid email.
2. Enter an invalid password.
3. Click Login.

### Expected Result

The system displays the message:

"Invalid email or password."

### Actual Result

The validation message is displayed.

### Status

PASS

---

## TC-LOGIN-003 - Login with Valid Credentials

### Preconditions

- User is on the Login screen.

### Test Data

Email: [qa@qace.com](mailto:qa@qace.com)

Password: 123456

### Steps

1. Enter valid credentials.
2. Click Login.

### Expected Result

The user is redirected to the Bug Dashboard.

### Actual Result

The Bug Dashboard is displayed.

### Status

PASS

---

## TC-LOGIN-004 - Logout

### Preconditions

- User is authenticated and on the Bug Dashboard.

### Steps

1. Click Logout.

### Expected Result

- User is redirected to the Login screen.
- Email field is cleared.
- Password field is cleared.
- Error messages are cleared.

### Actual Result

All expected behaviors were observed.

### Status

PASS
