# Search Test Cases

## TC-SEARCH-001 - Search by Bug Name

### Preconditions

- User is authenticated.
- User is on the Bug Dashboard.

### Steps

1. Enter "spider" in the search field.

### Expected Result

Only the "Crash Spider" bug card is displayed.

### Actual Result

Only the "Crash Spider" bug card is displayed.

### Status

PASS

---

## TC-SEARCH-002 - Search by Bug Family

### Preconditions

- User is authenticated.
- User is on the Bug Dashboard.

### Steps

1. Enter "beetle" in the search field.

### Expected Result

Only bug cards matching the Beetle family are displayed.

### Actual Result

The "Null Beetle" bug card is displayed.

### Status

PASS

---

## TC-SEARCH-003 - Search by Description

### Preconditions

- User is authenticated.
- User is on the Bug Dashboard.

### Steps

1. Enter "failure" in the search field.

### Expected Result

Bug cards with descriptions containing "failure" or related partial matches are displayed.

### Actual Result

The "Crash Spider" and "API Caterpillar" bug cards are displayed.

### Status

PASS

---

## TC-SEARCH-004 - Case Insensitive Search

### Preconditions

- User is authenticated.
- User is on the Bug Dashboard.

### Steps

1. Enter "SPIDER" in the search field.

### Expected Result

The search should ignore uppercase/lowercase differences and display the matching bug card.

### Actual Result

The "Crash Spider" bug card is displayed.

### Status

PASS

---

## TC-SEARCH-005 - Search with No Results

### Preconditions

- User is authenticated.
- User is on the Bug Dashboard.

### Steps

1. Enter a search term that does not match any bug, such as "xxxxxxxx".

### Expected Result

No bug cards are displayed.
The system displays the empty state message:

"No bugs found"

"Try another search term or change the severity filter."

### Actual Result

The empty state message is displayed.

### Status

PASS

---

## TC-SEARCH-006 - Search Combined with Severity Filter

### Preconditions

- User is authenticated.
- User is on the Bug Dashboard.

### Steps

1. Select the "Low" severity filter.
2. Enter "spider" in the search field.

### Expected Result

No bug cards are displayed because "Crash Spider" is not a Low severity bug.
The empty state message is displayed.

### Actual Result

The empty state message is displayed.

### Status

PASS

---

## TC-SEARCH-007 - Clear Search Field

### Preconditions

- User is authenticated.
- User is on the Bug Dashboard.
- A search term is currently applied.

### Steps

1. Clear the search field.

### Expected Result

The bug list is restored according to the currently selected severity filter.

### Actual Result

The bug list is restored correctly.

### Status

PASS
