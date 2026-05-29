# User Management

Create and manage user accounts from the Users page. Control access, enforce security policies, and manage your organization's users.

## Overview

The Users page allows Super Admins to:

- Create new user accounts
- Edit existing users
- Manage user permissions
- Enforce two-factor authentication
- Perform bulk actions

## Accessing Users

1. Click **Users** in the sidebar
2. The Users page displays all user accounts

## Key Features

| Feature | Description |
|---------|-------------|
| User List | View all users with status and role |
| Create User | Add new accounts |
| Edit User | Modify user settings |
| Bulk Actions | Perform actions on multiple users |
| Role Filtering | Filter by user type |
| 2FA Enforcement | Require TFA for users |

## User Types

GT AI OS has three user types:

| User Type | Access Level | Best For |
|-----------|--------------|----------|
| **Super Admin** | Full Control Panel access, all tenants | IT administrators, system managers |
| **Tenant Admin** | Manage users and settings within their tenant | Team leads, department managers |
| **Tenant User** | Chat, agents, datasets within their tenant | Regular team members |

### Permission Comparison

| Capability | Super Admin | Tenant Admin | Tenant User |
|------------|-------------|--------------|-------------|
| Access Control Panel | Yes | No | No |
| Manage all tenants | Yes | No | No |
| Manage tenant users | Yes | Yes | No |
| Create agents | Yes | Yes | Yes |
| Use chat | Yes | Yes | Yes |
| View billing | Yes | No | No |
| Configure SMTP | Yes | No | No |

## How To: Create a User

Add a new user account:

1. Navigate to **Users** page
2. Click **Create User** (top right)
3. Fill in the form:
   - **Email:** User's email address (must be unique)
   - **Full Name:** User's display name
   - **Password:** Initial password (or leave blank if SMTP configured)
   - **Confirm Password:** Re-enter password
   - **User Type:** Select appropriate role
   - **Tenant:** Select which tenant (for non-Super Admin users)
   - **Require TFA:** Check to enforce two-factor authentication
4. Click **Create User**

### With SMTP Configured

If SMTP is configured, you can leave the password blank:

1. User receives a welcome email
2. Email contains instructions and reset link
3. User sets their own password
4. User configures TFA on first login

### Without SMTP

Without SMTP, you must:

1. Set an initial password
2. Communicate password to user securely
3. User should change password on first login

## How To: Edit a User

Modify an existing user:

1. Navigate to **Users** page
2. Find the user in the list
3. Click the **Edit** button (pencil icon)
4. Update fields as needed:
   - **Full Name**
   - **User Type** (role)
   - **Tenant** assignment
   - **Status** (enable/disable)
   - **TFA Required**
5. Click **Save**

## How To: Delete a User

Remove a user account:

1. Navigate to **Users** page
2. Find the user in the list
3. Click the **three-dot menu** on that row
4. Click **Delete**
5. Confirm the deletion

**Note:** Deleted users cannot be recovered. Their conversations and data remain but are no longer accessible.

## How To: Reset a User's Password

If a user forgets their password:

### With SMTP Configured

1. User clicks "Forgot Password?" on login page
2. User enters their email
3. Reset link is sent (valid 15 minutes)
4. User sets new password

### Without SMTP

1. Navigate to **Users** page
2. Find the user
3. Click **Edit**
4. Set a new temporary password
5. Click **Save**
6. Communicate password to user securely

## How To: Reset User's TFA

If a user loses access to their authenticator:

1. Navigate to **Users** page
2. Find the user
3. Click the **three-dot menu**
4. Click **Reset TFA**
5. Confirm the action

User will need to set up TFA again on next login.

## Bulk Actions

Perform actions on multiple users at once:

1. Navigate to **Users** page
2. Select users using checkboxes
3. Choose action from the bulk actions menu:
   - **Disable Selected**
   - **Enable Selected**
   - **Require TFA**
   - **Delete Selected**
4. Confirm the action

## User List Filters

Filter the user list to find specific users:

| Filter | Options |
|--------|---------|
| **User Type** | All, Super Admin, Tenant Admin, Tenant User |
| **Status** | All, Active, Disabled |
| **Tenant** | All tenants or specific tenant |
| **TFA Status** | All, TFA Enabled, TFA Disabled |

## Security Best Practices

| Practice | Recommendation |
|----------|----------------|
| Delete default account | Remove `gtadmin@test.com` immediately |
| Require TFA for admins | All Super Admin and Tenant Admin accounts should have TFA |
| Use strong passwords | Enforce minimum 8 characters, letters + numbers |
| Regular review | Periodically review user list, disable unused accounts |
| Least privilege | Assign minimum required permissions |

## License Seat Management

Each active user consumes one license seat.

| User Status | Seat Usage |
|-------------|------------|
| Active | Consumes 1 seat |
| Disabled | Does not consume seat |
| Deleted | Does not consume seat |

### Freeing Seats

To free license seats:

1. Navigate to **Users** page
2. Find inactive users
3. Either:
   - **Disable** to preserve account but free seat
   - **Delete** to permanently remove

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Can't create user | Check license seat availability |
| Email already exists | Each email must be unique across all tenants |
| User can't log in | Verify status is Active, check password, verify TFA |
| TFA reset needed | Use Reset TFA from user menu |
| Forgot admin password | See [Troubleshooting](troubleshooting) |

### Common Issues

**"Cannot create more users"**
- You've reached your license seat limit
- Disable unused accounts or upgrade license

**"Email already in use"**
- That email exists in another tenant
- Each email can only be used once across the system

**"User locked out"**
- Check if account is disabled
- Reset TFA if authenticator lost
- Reset password if forgotten

## Next Steps

- [Email Settings](email-settings) - Configure welcome emails for new users
- [License Management](license-management) - Monitor seat usage
- [Troubleshooting](troubleshooting) - Resolve login issues
