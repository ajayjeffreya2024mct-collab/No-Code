# Experiment 3: Design of Test Cases and a Maintenance Plan for a Sample Software Module

## 1. Aim

To design test cases for a sample software module using standard testing techniques and to prepare a maintenance plan for it.

## 2. Objectives

- Apply black-box techniques: equivalence partitioning and boundary value analysis.
- Write structured test cases with expected results.
- Understand the types of software maintenance.
- Prepare a maintenance plan with schedule, responsibilities, and metrics.

## 3. Requirements

- Spreadsheet or Markdown editor
- Optional: Python 3 with `pytest` to automate selected test cases

## 4. Theory

### 4.1 Testing Techniques

| Technique | Idea |
|---|---|
| Equivalence partitioning | Divide inputs into classes expected to behave the same; test one value per class |
| Boundary value analysis | Test values at and around the edges of valid ranges |
| Decision table testing | Test combinations of conditions and resulting actions |
| Error guessing | Use experience to test likely failure points |

### 4.2 Test Case Components

Test case ID, description, preconditions, input data, steps, expected result, actual result, status.

### 4.3 Types of Maintenance

| Type | Purpose | Example |
|---|---|---|
| Corrective | Fix defects found after release | Fix incorrect login lockout |
| Adaptive | Adjust to environment changes | Support a new browser or OS version |
| Perfective | Improve performance or add features | Add "Forgot password" feature |
| Preventive | Reduce future problems | Refactor code, update libraries |

## 5. Sample Module: User Login

### 5.1 Requirements

| ID | Requirement |
|---|---|
| R1 | Username must be 5 to 15 alphanumeric characters |
| R2 | Password must be 8 to 20 characters, with at least one digit and one uppercase letter |
| R3 | Valid credentials grant access to the dashboard |
| R4 | Invalid credentials show an error message |
| R5 | Account is locked after 3 consecutive failed attempts |

### 5.2 Equivalence Classes

| Input | Valid Class | Invalid Classes |
|---|---|---|
| Username length | 5 to 15 | Fewer than 5; more than 15; empty |
| Username characters | Letters and digits | Special characters |
| Password length | 8 to 20 | Fewer than 8; more than 20; empty |
| Password rules | Has digit and uppercase | No digit; no uppercase |

### 5.3 Boundary Values

| Field | Boundary Test Values |
|---|---|
| Username length | 4, 5, 6, 14, 15, 16 |
| Password length | 7, 8, 9, 19, 20, 21 |
| Failed attempts | 2, 3, 4 |

### 5.4 Test Cases

| TC ID | Requirement | Description | Input | Expected Result |
|---|---|---|---|---|
| TC01 | R3 | Valid login | user: `john123`, pass: `Secure123` | Dashboard displayed |
| TC02 | R4 | Wrong password | user: `john123`, pass: `Wrong123` | Error: invalid credentials |
| TC03 | R4 | Unregistered username | user: `nouser99`, pass: `Secure123` | Error: invalid credentials |
| TC04 | R1 | Username too short (4) | user: `abcd`, pass: `Secure123` | Validation error: username length |
| TC05 | R1 | Username minimum length (5) | user: `abcde` (registered), pass: valid | Login succeeds |
| TC06 | R1 | Username maximum length (15) | 15-character registered username, valid pass | Login succeeds |
| TC07 | R1 | Username too long (16) | 16-character username | Validation error: username length |
| TC08 | R1 | Special characters in username | user: `john@123` | Validation error: invalid characters |
| TC09 | R1 | Empty username | user: empty, pass: valid | Validation error: required field |
| TC10 | R2 | Password too short (7) | pass: `Abcde12` | Validation error: password length |
| TC11 | R2 | Password minimum length (8) | pass: `Abcdef12` (registered) | Login succeeds |
| TC12 | R2 | Password too long (21) | 21-character password | Validation error: password length |
| TC13 | R2 | No digit in password | pass: `Abcdefgh` | Validation error: digit required |
| TC14 | R2 | No uppercase in password | pass: `abcdefg1` | Validation error: uppercase required |
| TC15 | R2 | Empty password | pass: empty | Validation error: required field |
| TC16 | R5 | Three consecutive failed logins | 3 wrong passwords in a row | Account locked, message shown |
| TC17 | R5 | Login attempt on locked account | Correct credentials after lock | Access denied, lock message |
| TC18 | R5 | Counter reset after success | 2 failures, then success | Login succeeds, counter resets |
| TC19 | Security | SQL injection attempt | user: `' OR '1'='1` | Rejected, no access |
| TC20 | Security | Password masked | Type password | Characters hidden |

### 5.5 Optional Automation (Python / pytest)

```python
# login_validation.py
import re

def validate_username(u: str) -> bool:
    return bool(re.fullmatch(r"[A-Za-z0-9]{5,15}", u))

def validate_password(p: str) -> bool:
    return (8 <= len(p) <= 20
            and any(c.isdigit() for c in p)
            and any(c.isupper() for c in p))
```

```python
# test_login_validation.py
import pytest
from login_validation import validate_username, validate_password

@pytest.mark.parametrize("username, expected", [
    ("abcd", False),            # 4 chars, below boundary
    ("abcde", True),            # 5 chars, lower boundary
    ("a" * 15, True),           # 15 chars, upper boundary
    ("a" * 16, False),          # 16 chars, above boundary
    ("john@123", False),        # special character
    ("", False),                # empty
])
def test_username(username, expected):
    assert validate_username(username) == expected

@pytest.mark.parametrize("password, expected", [
    ("Abcde12", False),         # 7 chars
    ("Abcdef12", True),         # 8 chars
    ("A1" + "b" * 18, True),    # 20 chars
    ("A1" + "b" * 19, False),   # 21 chars
    ("Abcdefgh", False),        # no digit
    ("abcdefg1", False),        # no uppercase
])
def test_password(password, expected):
    assert validate_password(password) == expected
```

Run with:

```bash
pip install pytest
pytest -v
```

### 5.6 Test Execution Record

| TC ID | Actual Result | Status (Pass/Fail) | Defect ID | Remarks |
|---|---|---|---|---|
| TC01 | | | | |
| TC02 | | | | |
| ... | | | | |

### 5.7 Requirements Traceability Matrix

| Requirement | Test Cases |
|---|---|
| R1 | TC04–TC09 |
| R2 | TC10–TC15 |
| R3 | TC01 |
| R4 | TC02, TC03 |
| R5 | TC16–TC18 |

## 6. Maintenance Plan

### 6.1 Scope and Objectives

Keep the login module secure, available, and compatible with changing platforms, with minimal downtime.

### 6.2 Maintenance Activities

| Type | Activity | Frequency | Owner |
|---|---|---|---|
| Corrective | Triage and fix reported defects | As reported; critical within 24 hours | Developer |
| Adaptive | Test with new browser/OS versions and API changes | Quarterly | Developer, Tester |
| Perfective | Enhancements (e.g., multi-factor authentication) | Per release cycle | Product owner, Developer |
| Preventive | Dependency updates, security scans, refactoring | Monthly | Developer |

### 6.3 Issue Severity and Response

| Severity | Definition | Target Response | Target Resolution |
|---|---|---|---|
| Critical | Users cannot log in / security breach | 1 hour | 24 hours |
| High | Major feature impaired | 4 hours | 3 days |
| Medium | Minor feature issue, workaround exists | 1 day | Next release |
| Low | Cosmetic | 3 days | Backlog |

### 6.4 Change Management

1. Log the request (bug or enhancement) in an issue tracker.
2. Analyze impact and estimate effort.
3. Approve and schedule.
4. Implement and run regression tests.
5. Review, deploy, and update documentation.

### 6.5 Regression Testing

Run the full login test suite (TC01–TC20) after every change. Automate the repeatable cases in a CI pipeline.

### 6.6 Maintenance Metrics

| Metric | Target |
|---|---|
| Mean time to repair (MTTR) | Under 8 hours for high severity |
| Defect escape rate | Under 5% |
| Availability | 99.5% or higher |
| Regression pass rate | 100% before release |

### 6.7 Documentation and Backup

- Maintain a changelog and version history.
- Keep design and test documents updated.
- Back up configuration and user data regularly; test recovery periodically.

## 7. Procedure

1. Choose a module (or use User Login) and list its requirements.
2. Identify equivalence classes and boundary values.
3. Write test cases and map them to requirements.
4. Execute the tests (manually or with pytest) and record results.
5. Prepare the maintenance plan covering the four maintenance types.

## 8. Observations

Record pass/fail counts and any defects found.

| Total Test Cases | Passed | Failed | Defects Raised |
|---|---|---|---|
| | | | |

## 9. Result

Test cases were designed using equivalence partitioning and boundary value analysis, and a maintenance plan was prepared for the sample module.

## 10. Conclusion

Systematic test design improves defect detection, while a maintenance plan keeps the software reliable and adaptable after release.

## 11. Viva Questions

1. Differentiate between equivalence partitioning and boundary value analysis.
2. What is a requirements traceability matrix?
3. Name the four types of maintenance with examples.
4. What is regression testing and why is it important?
5. How is severity different from priority?
