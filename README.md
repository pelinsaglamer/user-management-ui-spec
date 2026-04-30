# User Interface Specification Document  
## User Management Screen

---

## 1. Introduction

This document defines the complete user interface specification for the **User Management Screen** shown in the provided mockup.  
The purpose of this screen is to allow authorized administrators to:

- View existing users
- Filter users
- Create new users
- Edit existing users
- Assign user roles
- Enable or disable user accounts
- Save user profile information

This specification will be used by software developers to implement the screen behavior, UI logic, field validations, and user interactions.

---

## 2. Screen Purpose

The User Management Screen is designed as an administrative panel for managing application users.

The page contains two main sections:

1. **User Listing Panel (Left Side)**  
   Displays all registered users in a table.

2. **User Detail Form Panel (Right Side)**  
   Displays selected user information or empty fields for creating a new user.

---

## 3. Initial Page Load Behavior

When the page is opened, the following behavior must occur:

- All active users are loaded from the database.
- Disabled users are hidden by default if "Hide Disabled User" checkbox is checked.
- The user list table is populated on the left side.
- The first user in the table is automatically selected.
- Selected user details are displayed in the detail form on the right side.
- The "Save User" button is visible but inactive until data is changed.
- "New User" button is enabled.

---

## 4. Layout Structure

The screen shall be divided horizontally into two panels:

| Panel | Width | Description |
|-------|-------|-------------|
| Left Panel | 45% | User list grid |
| Right Panel | 55% | User detail form |

---

## 5. UI Components Specification

---

### 5.1 New User Button

**Label:** `+ New User`

**Position:** Top left above user table.

**Behavior:**

When clicked:

- Clears all input fields on the right panel.
- Sets form mode to "Create New User".
- No row remains selected in the left table.
- Save User button becomes active after user enters data.

---

### 5.2 Hide Disabled User Checkbox

**Label:** `Hide Disabled User`

**Default State:** Checked

**Behavior:**

- If checked → only enabled users are shown in the table.
- If unchecked → all users including disabled users are shown.

The table refreshes immediately after checkbox value changes.

---

### 5.3 User List Table

The table shall contain the following columns:

| Column Name | Type | Description |
|-------------|------|-------------|
| ID | Integer | Unique user identifier |
| User Name | Text | System username |
| Email | Text | User email address |
| Enabled | Boolean | Indicates whether account is active |

#### Table Functional Requirements

- Rows must be selectable by single click.
- Selected row must be highlighted.
- Clicking a row loads user details into the form.
- Columns should support sorting ascending/descending.
- Filter icon should allow searching by column value.

---

### 5.4 Save User Button

**Label:** `Save User`

**Position:** Top right corner of detail panel.

**Behavior:**

When clicked:

- Validate all required fields.
- If validation passes, save data into database.
- If user is new → insert record.
- If existing user → update record.
- Refresh user table.
- Show success notification.

---

## 6. User Detail Form Fields

---

### 6.1 Username Field

- Type: Textbox
- Required: Yes
- Max Length: 50 characters
- Must be unique

Validation:

- Cannot be empty
- Cannot contain spaces
- Duplicate usernames are not allowed

---

### 6.2 Display Name Field

- Type: Textbox
- Required: Yes
- Max Length: 100 characters

Validation:

- Cannot be empty

---

### 6.3 Phone Field

- Type: Textbox
- Required: No

Validation:

- Accept numeric characters, "+" and "-"
- Maximum 20 characters

---

### 6.4 Email Field

- Type: Textbox
- Required: Yes

Validation:

- Must contain valid email format
- Duplicate emails should not be allowed

Example valid format:

user@example.com

---

### 6.5 User Roles Dropdown

- Type: Multi-select dropdown list

Available options:

- Guest
- Admin
- SuperAdmin

Behavior:

- One or more roles may be selected.
- Selected roles should remain highlighted.

Validation:

- At least one role must be selected.

---

### 6.6 Enabled Checkbox

- Type: Checkbox

Behavior:

- Checked = user account is active
- Unchecked = user account is disabled

Disabled users should not appear in list when "Hide Disabled User" is enabled.

---

## 7. User Interaction Flow

### Scenario A: Viewing Existing User

1. User opens page
2. Existing users are shown
3. User clicks one row
4. Detail form displays selected user information

---

### Scenario B: Creating New User

1. User clicks `+ New User`
2. Empty form appears
3. User enters all required information
4. User selects role(s)
5. User checks Enabled if account should be active
6. User clicks Save User
7. System validates input
8. System inserts new user record
9. New user appears in table

---

### Scenario C: Updating Existing User

1. User selects an existing user
2. User edits one or more fields
3. User clicks Save User
4. System validates input
5. System updates user record
6. Table refreshes

---

## 8. Validation Rules Summary

| Field | Required | Validation Rule |
|-------|----------|-----------------|
| Username | Yes | Unique, no spaces |
| Display Name | Yes | Cannot be empty |
| Phone | No | Valid characters only |
| Email | Yes | Valid email format, unique |
| User Roles | Yes | Minimum one role |
| Enabled | No | Boolean only |

---

## 9. Error Handling

The system must display user-friendly error messages.

Examples:

- "Username is required."
- "Username already exists."
- "Display Name is required."
- "Invalid email format."
- "Email already exists."
- "Please select at least one user role."

Errors should appear directly below the related field or as a notification popup.

---

## 10. Success Handling

After successful save:

- Show message: `User saved successfully.`
- Refresh left panel table.
- Keep saved user selected.

---

## 11. Non-Functional Requirements

- Screen should load within 2 seconds.
- Form should support responsive resizing.
- All buttons must be clickable on standard desktop browsers.
- Keyboard tab navigation should be supported.
- Text fields must support copy/paste.

---

## 12. Accessibility Notes

- Labels must be visible for each input.
- Checkbox states must be visually clear.
- Selected row should be highlighted with contrast color.
- Error messages should be readable.

---

## 13. Technical Recommendation for Developers

Suggested Frontend Technologies:

- HTML5
- CSS3
- JavaScript / TypeScript
- React / Angular / Vue (optional)
- REST API integration for CRUD operations

Suggested Backend Functionalities:

- GET Users
- GET User By ID
- CREATE User
- UPDATE User
- FILTER Enabled Users

---

## 14. Conclusion

This screen provides complete administrative user management functionality including:

- user listing,
- user creation,
- user editing,
- role assignment,
- enable/disable management,
- filtering and validation.

The software development team should implement all described UI behaviors, validations, and user workflows exactly as specified in this document.

---
