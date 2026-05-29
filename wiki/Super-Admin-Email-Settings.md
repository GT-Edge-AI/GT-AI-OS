# Email Settings

Configure SMTP for password reset emails, welcome emails, and system notifications. Email functionality is essential for Enterprise features.

## Overview

The Email Settings page allows Super Admins to:

- Configure SMTP server connection
- Test email delivery
- Customize email templates
- Manage welcome email settings
- Configure broadcast notifications

## Accessing Email Settings

1. Click **Email Settings** in the sidebar
2. The page displays SMTP configuration and template options

## Key Features

| Feature | Description |
|---------|-------------|
| SMTP Configuration | Server connection settings |
| Test Email | Verify configuration works |
| Welcome Emails | Automatic emails for new users |
| Email Templates | Customize email content |
| CC Recipients | Copy emails to administrators |

## SMTP Configuration

### Required Settings

Configure these fields to enable email:

| Field | Description | Example |
|-------|-------------|---------|
| **SMTP Host** | Email server address | `smtp.gmail.com` |
| **SMTP Port** | Connection port | `587` |
| **Username** | Authentication username | `noreply@yourcompany.com` |
| **Password** | Authentication password | Your password or app password |
| **From Email** | Sender email address | `noreply@yourcompany.com` |
| **From Name** | Sender display name | `GT AI OS` |
| **Use TLS** | Enable encryption | Enabled (recommended) |

### How To: Configure SMTP

1. Navigate to **Email Settings**
2. Select the **SMTP Configuration** tab
3. Enter your server details
4. Click **Save**
5. Click **Send Test Email** to verify

**Note:** Password is encrypted before storage. Leave blank when updating to keep existing password.

## Common Provider Settings

### Gmail

| Setting | Value |
|---------|-------|
| Host | `smtp.gmail.com` |
| Port | `587` |
| TLS | Enabled |
| Username | Your full Gmail address |
| Password | **App Password** (not regular password) |

**Creating Gmail App Password:**
1. Go to https://myaccount.google.com/apppasswords
2. Sign in with 2-Step Verification enabled
3. Select "Mail" and your device
4. Click "Generate"
5. Use the 16-character password

### Microsoft 365 / Outlook

| Setting | Value |
|---------|-------|
| Host | `smtp.office365.com` |
| Port | `587` |
| TLS | Enabled |
| Username | Your full email address |
| Password | Your password or app password |

### Amazon SES

| Setting | Value |
|---------|-------|
| Host | `email-smtp.{region}.amazonaws.com` |
| Port | `587` |
| TLS | Enabled |
| Username | SES SMTP username (from IAM) |
| Password | SES SMTP password (from IAM) |

**Note:** Verify your domain and email addresses in SES first.

### SendGrid

| Setting | Value |
|---------|-------|
| Host | `smtp.sendgrid.net` |
| Port | `587` |
| TLS | Enabled |
| Username | `apikey` |
| Password | Your SendGrid API key |

## How To: Test Email Configuration

Verify your SMTP settings work:

1. Navigate to **Email Settings**
2. Find **Send Test Email** section
3. Enter your email address
4. Click **Send Test Email**
5. Check your inbox (and spam folder)

### Test Results

| Result | Meaning |
|--------|---------|
| **Success** | SMTP configured correctly |
| **Auth Failed** | Username or password incorrect |
| **Connection Failed** | Cannot reach SMTP server |
| **SMTP Error** | Server rejected the email |

## Password Reset Emails

With SMTP configured, password reset works automatically:

1. User clicks "Forgot Password?" on login
2. User enters their email
3. System sends reset link (valid 15 minutes)
4. User clicks link and sets new password

### Security Features

| Feature | Description |
|---------|-------------|
| Token Encryption | AES-256 encrypted tokens |
| 15-Minute Expiry | Tokens expire quickly |
| Rate Limiting | 5 requests per email per hour |
| Audit Logging | All resets are logged |

## Welcome Email Configuration

Configure automatic emails for new users:

### Accessing Welcome Email Settings

1. Navigate to **Email Settings**
2. Select the **Welcome Email** tab

### Settings

| Setting | Description |
|---------|-------------|
| **Enabled** | Toggle welcome emails on/off |
| **Subject** | Email subject line |
| **Body** | Email content |
| **CC Emails** | Additional recipients |

### Available Placeholders

Use these in subject or body:

| Placeholder | Replaced With |
|-------------|---------------|
| `{user_name}` | User's full name |
| `{tenant_name}` | Organization name |
| `{login_url}` | Tenant App login URL |

### Default Template

**Subject:**
```
GT AI OS Welcome Email for {user_name} | {tenant_name}
```

**Body:**
```
Welcome to the GT Edge AI service!

To access the platform please go to: {login_url}

Login Instructions:
1. Click "Forgot Password?" and enter your email
2. Click the reset link in your email
3. Set your password
4. Log in with your email and new password
5. Set up Two-Factor Authentication

Support: support@gtedge.ai
```

## Email Templates

Customize various email templates:

### Available Templates

| Template | When Sent |
|----------|-----------|
| **Welcome** | When new user is created |
| **Password Reset** | When password reset requested |
| **Invite** | When user is invited to team |
| **Broadcast** | Admin-initiated announcements |

### How To: Edit Templates

1. Navigate to **Email Settings**
2. Select the **Email Templates** tab (or navigate to Email Templates page)
3. Select the template to edit
4. Modify subject and body
5. Use placeholders as needed
6. Click **Save**

## Adding CC Recipients

Send copies of emails to administrators:

1. Navigate to **Email Settings**
2. Select the **Welcome Email** tab
3. Find **CC Emails** section
4. Click **Add**
5. Enter administrator email address
6. Click **Save**

All welcome emails will be copied to these addresses.

## Troubleshooting

### "Test email not received"

| Check | Solution |
|-------|----------|
| Spam folder | Check junk/spam folder |
| From address | Must be authorized for your SMTP server |
| Credentials | Verify username and password |
| Different recipient | Try a different email address |

### "Authentication failed"

| Provider | Fix |
|----------|-----|
| Gmail | Use App Password, not regular password |
| Office 365 | Enable "Authenticated SMTP" in admin portal |
| Others | Verify username format (full email vs username) |

### "Connection failed"

| Cause | Solution |
|-------|----------|
| Wrong host | Verify SMTP host address |
| Wrong port | Try 587 (TLS) or 465 (SSL) |
| Firewall | Ensure outbound port is open |
| TLS mismatch | Toggle "Use TLS" setting |

### "Password reset not sending"

1. Verify SMTP is configured and tested
2. Check user exists and is active
3. Wait if rate limited (5 requests/hour)
4. Check backend logs for errors

### Checking Logs

```bash
# View SMTP-related logs
docker compose logs control-panel-backend --tail 100 | grep -i smtp

# View email-related logs
docker compose logs control-panel-backend --tail 100 | grep -i email
```

## Security Best Practices

| Practice | Recommendation |
|----------|----------------|
| Dedicated email | Don't use personal email for system emails |
| App passwords | Never use main account password |
| Enable TLS | Always use encrypted connections |
| Monitor delivery | Verify users receive emails |
| Review logs | Check for failed delivery attempts |

## Next Steps

- [User Management](user-management) - Create users with welcome emails
- [Deployment Checklist](deployment-checklist) - Complete initial setup
- [Troubleshooting](troubleshooting) - Resolve email issues
