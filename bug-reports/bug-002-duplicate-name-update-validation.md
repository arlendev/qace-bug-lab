# BUG-002 - Update Form Allows Duplicate Bug Names

## Summary

The bug update form allows an existing bug to be renamed using a name that already exists in the system.

Although duplicate bug names are correctly prevented during bug creation, the same validation is not applied when editing an existing bug.

This results in inconsistent behavior between the Create Bug and Update Bug workflows and allows duplicate records to be stored.

---

## Severity

Medium

---

## Priority

Medium

---

## Environment

* Application: QAce Bug Lab
* Version: Current Development Version
* Browser: Google Chrome
* Platform: Windows 11

---

## Preconditions

* User is logged in.
* At least two different bugs already exist.
* User is on the dashboard.

---

## Steps to Reproduce

1. Create two bugs with different names.

Example:

* Bug Alpha
* Bug Beta

2. Open **Bug Beta** for editing.
3. Change its name to **Bug Alpha**.
4. Click **Save Bug**.

---

## Expected Result

The application should reject the update and display a validation message informing the user that the bug name already exists.

The validation rule should be identical to the one applied during bug creation.

---

## Actual Result

The application accepts the duplicate name and successfully updates the record.

Two bugs with the same name are then displayed on the dashboard.

---

## Impact

* Creates duplicate bug records.
* Introduces inconsistent validation rules.
* Reduces data integrity.
* Makes bug identification more difficult.
* May negatively impact future search, reporting and maintenance activities.

---

## Evidence

The following behavior was observed during exploratory testing:

* Creating a bug with an existing name is correctly rejected.
* Updating an existing bug using an already existing name is accepted.

This demonstrates inconsistent validation between the Create Bug and Update Bug workflows.

---

## Status

Open

---

## QA Notes

This defect was identified during exploratory testing by comparing the validation rules implemented in different application workflows.

The Create Bug form correctly prevents duplicate bug names, while the Update Bug form does not enforce the same business rule.

This inconsistency allows duplicate records to be created after editing existing bugs and may compromise data integrity over time.