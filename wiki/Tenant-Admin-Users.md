# User Management

As a Tenant Admin, you can manage users within your organization. This guide covers all aspects of user management.

## Overview

User management allows you to:
- Add new users individually or in bulk via CSV upload
- Control user access (enable/disable accounts)
- Manage two-factor authentication settings
- View user activity and status
- Monitor license usage and expiration

## Page Layout

The Users page displays:

### Stats Dashboard

Four cards at the top show key metrics:
- **Enabled Users (License)**: Current active users vs. your license limit. A warning appears when the limit is reached.
- **Total Users**: All users (enabled + disabled)
- **Disabled**: Users who have been disabled
- **License Expires**: Your license expiration date. The card turns amber when expiring within 30 days, or red if expired.

### Search and User Table

Below the dashboard:
- **Search bar**: Filter users by name or email
- **User table** with columns:
  - **User**: Name, email, and role badge (if admin)
  - **Status**: Enabled or Disabled
  - **2FA**: Enabled, Required, or Not Set
  - **Last Login**: When the user last logged in
  - **Actions**: Menu for user management actions

## User Roles

### Understanding Roles

| Role | Description | Capabilities |
|------|-------------|--------------|
| **Tenant User** | Standard user | Use agents, manage personal resources |
| **Tenant Admin** | Platform administrator | All user capabilities plus admin features |
| **Super Admin** | System administrator | Full platform access across all tenants |

**Note**: Super Admin users are managed through the Control Panel by a Super Admin, not the tenant app. They appear in your user list for visibility but cannot be edited or disabled from this page.

### Role Capabilities

**Tenant Users can:**
- Access the chat interface
- Use available agents
- Create personal agents and datasets
- Join teams and use team resources
- View their own usage and history

**Tenant Admins can additionally:**
- Access the Users management page
- Add and disable users
- Bulk upload users via CSV
- Access organization-wide **Observability**
- See all resources regardless of visibility
- Set resource visibility to **Organization** (making resources available to all users)

## Adding Users

### Adding a Single User

1. Go to **Users** in the sidebar
2. Click **Add User**
3. Enter the user's information:
   - **First Name**: The user's first name (required)
   - **Last Name**: The user's last name (required)
   - **Email Address**: The user's email (required)
   - **Welcome Email Template**: Select a template for the welcome email (optional)
   - **Email Modules**: Select header/footer modules to include (optional)
   - **Require 2FA**: Toggle to require two-factor authentication
4. Click **Create User**

**Note**: Tenant Admins can only create Tenant Users. Tenant Admin roles can only be provisioned by a Super Admin through the Control Panel.

### Bulk Upload via CSV

To add multiple users at once:

1. Go to **Users** in the sidebar
2. Click **Bulk Upload**
3. Optionally click **Download CSV Template** to get a pre-formatted file
4. Prepare your CSV file with the following columns:

```
email,first_name,last_name,tfa_required
jane.doe@example.com,Jane,Doe,false
john.smith@example.com,John,Smith,true
```

5. Click the upload area to select your CSV file
6. Click **Upload**

After the upload completes, a summary shows:
- Number of users successfully created
- Number of rows that failed (with specific error details per row)

Passwords are auto-generated for all uploaded users. Each user receives a welcome email with instructions to set up their password.

### What Happens Next

After creating a user (individually or via bulk upload):
1. The user receives a welcome email with instructions to set up their password
2. They click the link in the email to create their password
3. If 2FA is required, they set it up on first login

## Managing Existing Users

### User Table

The table displays all users with their current status. Each row shows:
- User avatar with name and email
- Role badge (for admins)
- Status badge (Enabled/Disabled)
- 2FA status
- Last login time
- Actions menu (for non-admin users)

**Note**: Tenant Admin and Super Admin users show "Admin (read-only)" instead of an actions menu. These roles can only be managed through the Control Panel by a Super Admin.

### Editing a User

1. Find the user in the table
2. Click the actions menu (**...**) on the right
3. Select **Edit**
4. The edit panel opens from the right side
5. You can:
   - Update the user's **First Name** and **Last Name**
   - **Disable User** or **Enable User** (in Quick Actions)
   - **Require 2FA** or **Remove 2FA Requirement** (in Quick Actions)
   - View the **2FA Status** section showing the current state:
     - "2FA is enabled and active" — the user has set up 2FA
     - "2FA is required but not yet set up" — 2FA is required but the user hasn't completed setup
     - "2FA is not configured" — 2FA is not set up or required
6. Click **Save Changes**

**Note**: If your organization has a global 2FA policy enabled, the edit panel shows "2FA Required — Enforced by organization policy" and the remove option is hidden.

### User Role Information

User roles are displayed in the user table:
- **Tenant User**: Standard users with access to chat, agents, and datasets
- **Tenant Admin**: Platform administrators with access to user management and full observability

**Note**: Tenant Admin roles can only be provisioned by a Super Admin through the Control Panel. They cannot be assigned in the tenant app.

## Disabling Users

### How to Disable a User

From the user table:
1. Find the user in the list
2. Click the actions menu (**...**)
3. Select **Disable**

Or from the edit panel:
1. Open the edit panel for the user
2. Click **Disable** in the Quick Actions section

**Note**: Disabled users cannot log in but their data is preserved. This action is reversible - you can re-enable the user later.

### Re-enabling a User

Use the actions menu and select **Enable**, or use the **Enable** button in the edit panel.

## User Access Control

### Password Management

To send a password reset email:
1. Find the user in the table
2. Click the actions menu (**...**)
3. Select **Send Password Reset**

The user will receive an email with a link to reset their password.

### Two-Factor Authentication (2FA)

Manage 2FA settings for users from the actions menu:

| Action | Description |
|--------|-------------|
| **Require 2FA** | User must set up 2FA on their next login |
| **Disable 2FA Requirement** | Remove the 2FA requirement (if not globally enforced) |
| **Reset 2FA** | Clear the user's 2FA so they can set up a new device |

**Note**: If your organization has a global 2FA policy, individual settings cannot override it. The "Disable 2FA Requirement" option will not appear for users when global 2FA is enforced.

### Account Status

Monitor user account status:
- **Enabled**: User can log in normally
- **Disabled**: A Tenant Admin has disabled the account

## Best Practices

### Onboarding New Users

For a single user:
1. Create their account via **Add User**
2. Verify they received the welcome email
3. Point them to help documentation
4. Assign them to relevant teams
5. Follow up to ensure successful setup

For multiple users:
1. Prepare a CSV file with all user details
2. Use **Bulk Upload** to create all accounts at once
3. Review the upload results for any errors
4. Verify users received their welcome emails

### Regular Maintenance

- Review user list quarterly
- Disable inactive users
- Monitor the **License Expires** card for upcoming renewals
- Update contact information as needed

### Security Considerations

- Review access logs regularly
- Promptly disable departing employees
- Report suspicious activity to your Super Admin

## Troubleshooting

### User Can't Log In

Check:
1. Account status is Enabled (not Disabled)
2. Email address is correct
3. Password meets requirements

### Password Reset Not Working

If the user isn't receiving password reset emails:
1. Verify SMTP is configured for your tenant
2. Check spam/junk folders
3. Verify the email address is correct
4. Contact your Super Admin if SMTP issues persist

### Bulk Upload Errors

If rows fail during bulk upload:
- Check the error details shown for each failed row
- Common issues: duplicate email addresses, invalid email format, missing required fields
- Fix the errors in your CSV and re-upload only the failed rows

### Missing User

If a user doesn't appear in the list:
1. Use the search bar to search by email
2. Verify the user was created successfully
3. Check if they were accidentally disabled (they still appear in the list)
