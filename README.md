

## What the page looks like

The page is basically two halves sitting side by side.

On the left you've got a table of all the users in the system. On the right you've got a form for creating or editing a user. Above both of them is a toolbar with a couple of controls.

```
[ + New User ]  [ ✓ Hide Disabled User ]             [ Save User ]
-----------------------------------------------------------------------
|  ID | User Name  | Email              | Enabled  |  New User        |
|-----|------------|--------------------|--------- |                  |
|  1  | AdminUser  | admin@piworks.net  | true     |  Username: ____  |
|  2  | Test User  | test@piworks.net   | true     |  Display Name:   |
|     |            |                    |          |  Phone:          |
|     |            |                    |          |  Email:          |
|     |            |                    |          |  User Roles:     |
|     |            |                    |          |  Enabled: [ ]    |
```

---

## When you first open the page

- The table shows only **enabled** users. The "Hide Disabled User" checkbox is checked by default, so disabled accounts don't clutter the list.
- The form on the right is blank and titled **"New User"** — ready for input.
- The **Save User** button is up in the top right. It should be greyed out / disabled until the required fields are filled in.

---

## The toolbar

### "+ New User" button (top left)

Pretty self-explanatory — clicking this clears the form and resets it back to the blank "New User" state. Useful if you've clicked on a user to edit them but then change your mind and want to create someone new instead.

If there are unsaved changes in the form when they click this, it'd be nice to show a quick confirmation ("You have unsaved changes, are you sure?") but that's up to you — not a hard requirement.

### "Hide Disabled User" checkbox (top left, next to the button)

Checked by default. When it's checked, only users with `enabled = true` show up in the table. Uncheck it and you see everyone including disabled accounts. This should filter the table instantly — no page refresh needed.

### "Save User" button (top right)

This button handles both creating and updating depending on the context:

- If the form is in "New User" mode → creates a new user
- If you've selected a user from the table → saves updates to that user

On success, show a quick success message (toast/snackbar is fine) and refresh the table so the changes show up. On failure, show an error with some indication of what went wrong — don't just silently fail.

---

## The user table (left side)

### Columns

| Column | Sortable? | Filterable? |
|--------|-----------|-------------|
| ID | yes | no |
| User Name | yes | yes |
| Email | yes | yes |
| Enabled | yes | no |

The sort icons (↑↓) next to each column header cycle through ascending → descending → back to default. Only one column sorted at a time. Default is ID ascending.

The filter icon (the funnel) next to User Name and Email lets you type to filter those columns. It should filter as you type, case-insensitive.

### Clicking a row

When you click a row in the table, two things happen:
1. The row highlights to show it's selected
2. The form on the right fills in with that user's data and the form title changes to the user's name (e.g. "AdminUser" instead of "New User")

From there you can edit the fields and hit Save User to update them. Only one row can be selected at a time — clicking a different row switches the form to that user.

### Empty state

If there's nothing to show (e.g. all users are disabled and the filter is on), just display something like "No users found." in the table body.

---

## The user form (right side)

This form is used for both creating and editing. The title at the top either says "New User" or the name of whoever you've selected.

### Fields

**Username** *(required)*  
Plain text input. Has to be unique — if someone tries to save with a duplicate username, show an inline error under the field. Probably cap it at 50 characters.

**Display Name** *(optional)*  
Plain text input. This is just the human-readable name shown around the app, doesn't need to be unique.

**Phone** *(optional)*  
Plain text input. If filled in, should be a valid phone number format — but don't over-engineer the validation here, a basic sanity check is fine.

**Email** *(required)*  
Standard email input. Has to be a valid format and unique. Show an inline error on save if it's already taken or malformed.

**User Roles** *(optional)*  
Multi-select dropdown. The placeholder text is "Select user roles..." and the available options are:

- Guest — basically read-only
- Admin — standard admin stuff
- SuperAdmin — full access, including this screen

You can pick more than one role. The dropdown stays open while selecting (as shown in the mockup — Guest is highlighted in blue). Once you've picked your roles, they should show up inside the field as tags or comma-separated text.

**Enabled** *(checkbox)*  
Unchecked by default for new users. If you check this, the account is active. If it's unchecked, the account is disabled and will be hidden from the table when the filter is on.

When editing an existing user, this checkbox should reflect whatever their current status is.

---

## Edge cases worth noting

- If you're editing a user and click "+ New User", the form resets. Any unsaved edits are gone.
- If you save a new user successfully, the form should reset to blank "New User" state (don't leave the new user selected).
- If validation fails on save, don't clear the form — leave everything as-is so the user can fix the errors.
- The table should update after every save without a full page reload.

---

## Questions / things to confirm

A few things I wasn't 100% sure about from the mockup alone:

- Should the "Save User" button be disabled until required fields are filled, or just validate on click?
- Is there a delete/deactivate user option somewhere, or is setting Enabled = false the way to "remove" someone?
- Are the role permissions (Guest vs Admin vs SuperAdmin) enforced on the backend, or does this screen just store the label?
- Any pagination needed on the table, or is the user count small enough that we can load everything at once?

---

That's pretty much it. The mockup covers most of the visual design — this doc is mainly to fill in the behavior and edge cases that aren't obvious from the screenshot.
