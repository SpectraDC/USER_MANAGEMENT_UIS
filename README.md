# USER_MANAGEMENT_UIS
USER_MANAGEMENT_UIS For Technical assignment 

Page Initialization
Default State: The page loads with a split-view layout. The left side contains the user list table, and the right side contains the "New User" form.

Initial Data: The user table should populate with existing active users by default.

Checkbox State: The "Hide Disabled User" checkbox is checked by default.

UI Components & Requirements
3.1 Global Actions (Top Bar)
"+ New User" Button: A blue button located at the top left. Clicking this clears any active selection in the table and resets the right-hand form to "New User" mode.

"Hide Disabled User" Checkbox: When toggled, the table should dynamically filter to exclude or include users where "Enabled" is false.

"Save User" Button: A blue button at the top right. This triggers a validation check of the current form fields before sending a POST/PUT request to the backend.

User Table (Left Panel)
The table displays user records with the following columns:

ID: Numeric identifier. Includes sort icons (up/down) and a filter icon.

User Name: Text display. Includes sort and filter icons.

Email: Text display. Includes sort and filter icons.

Enabled: Boolean status (true/false). Includes sort and filter icons.

Selection Behavior: Clicking a row highlights it in light blue and populates the right-hand form with that user's specific data for editing.

User Details Form (Right Panel)
The form title changes based on context (e.g., "New User" or "Edit User").

Username: Required text input.

Display Name: Required text input.

Phone: Optional text input (should follow standard phone formatting).

Email: Required text input with email regex validation.

User Roles: A multi-select dropdown. Options include Guest, Admin, and SuperAdmin.

Enabled Checkbox: Toggles the active status of the user.

Interaction Behavior
Sorting/Filtering: Clicking the icons in the table header should trigger client-side or server-side sorting/filtering for that specific column.

Form Validation: Upon clicking "Save User," the system must verify that required fields are not empty and that the email format is valid. Error messages should appear under the relevant fields if validation fails.
