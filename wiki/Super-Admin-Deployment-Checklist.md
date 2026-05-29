# Deployment Checklist

This checklist ensures your GT AI OS installation is secure and fully configured. Complete these steps in order after installation.

## Overview

A fresh installation uses default credentials that are publicly known. This checklist guides you through securing the installation and configuring essential features.

## Pre-Flight Verification

Before starting configuration, verify the installation is working:

| Check | How to Verify |
|-------|---------------|
| Control Panel accessible | Open http://localhost:3001 |
| Default login works | Sign in with `gtadmin@test.com` / `Test@123` |
| All containers running | Run `docker compose ps` - should show ~10 healthy containers |

## Step 1: Create Your Admin Account

Create your own Super Admin account before doing anything else.

1. Click **Users** in the sidebar
2. Click **Create User** (top right)
3. Fill in the form:
   - **Email:** Your email address
   - **Full Name:** Your full name
   - **Password:** Strong password (8+ characters, letters + numbers)
   - **Confirm Password:** Same password
   - **User Type:** Select **Super Admin**
   - **Require TFA:** Check this box
4. Click **Create User**
5. Verify your user appears in the list with "Super Admin" badge

## Step 2: Verify Your New Account

Before deleting the default account, confirm your new account works.

1. Click **Logout** (user menu, top right)
2. Sign in with YOUR new credentials
3. If prompted, set up TFA (see Step 4)
4. Verify you can see the Control Panel

**If login fails:** Sign in with default credentials and check your new user was created correctly.

## Step 3: Delete Default Admin

Now that your account works, remove the default account for security.

1. Click **Users** in the sidebar
2. Find `gtadmin@test.com` in the list
3. Click the **three-dot menu** on that row
4. Click **Delete**
5. Confirm the deletion

**After this step:** Default credentials will no longer work. Make sure you remember your new credentials.

## Step 4: Enable Two-Factor Authentication

If you didn't set up TFA during first login, do it now.

1. Click **Settings** in the sidebar
2. Find the **Two-Factor Authentication** section
3. Click **Enable TFA**
4. Scan the QR code with your authenticator app:
   - Google Authenticator
   - Microsoft Authenticator
   - Authy
   - 1Password
5. Enter the 6-digit code from your app
6. Click **Verify**

**Verification:** Next login will require your 6-digit code after password.

## Step 5: Configure SMTP (Email)

SMTP enables password reset and welcome emails. Required for Enterprise functionality.

1. Click **Email Settings** in the sidebar
2. Enter your SMTP server details:

| Field | Example |
|-------|---------|
| SMTP Host | `smtp.gmail.com` |
| SMTP Port | `587` |
| Username | `noreply@yourcompany.com` |
| Password | Your SMTP password or app password |
| From Email | `noreply@yourcompany.com` |
| From Name | `GT AI OS` |
| Use TLS | Enabled |

3. Click **Save**
4. Click **Send Test Email**
5. Enter your email and verify you receive the test

**For Gmail:** Use an App Password from https://myaccount.google.com/apppasswords

See [Email Settings](email-settings) for detailed configuration.

## Step 6: Activate Your License

Activate your Enterprise license to unlock unlimited users and advanced features.

1. Click **License** in the sidebar
2. Find and copy your **Deployment ID**
3. Contact GT Edge AI support with your Deployment ID
4. When you receive your license, paste it in the **License Activation** textarea
5. Click **Activate License**
6. Verify your license details appear (max seats, expiration)

See [License Management](license-management) for detailed instructions.

## Step 7: Add AI Provider API Keys

Configure at least one AI provider to enable chat functionality.

### Option A: NVIDIA NIM (Recommended)

1. Get API key from https://build.nvidia.com/
2. Click **Models** in sidebar
3. Click the **Inference Providers** tab
4. Click **Add Provider**
5. Select **NVIDIA** and paste your API key
6. Click **Save** and **Test**

### Option B: Groq

1. Get API key from https://console.groq.com/
2. Click **Models** > **Inference Providers** > **Add Provider**
3. Select **Groq** and paste your API key (starts with `gsk_`)
4. Click **Save** and **Test**

### Option C: Ollama (Local)

1. Install Ollama: https://ollama.com/download
2. Pull a model: `ollama pull dolphin3`
3. Click **Models** > **Configured Models** tab > **Add Model**
4. Configure:
   - **Model ID:** `dolphin3`
   - **Provider:** `Local Inference (Manual)`
   - **Endpoint URL:** `http://host.docker.internal:11434/v1/chat/completions`
5. Click **Save**

## Step 8: Update Tenant Settings

Configure your organization's tenant settings.

1. Click **Tenants** in the sidebar
2. Find your tenant (default: "GT AI OS")
3. Click the **Edit** button (pencil icon)
4. Update:
   - **Name:** Your organization name
   - **Frontend URL:** Your Tenant App URL (default: `http://localhost:3002`)
5. Click **Save**

## Summary Checklist

Before moving to the Tenant App, verify:

- [ ] Created your own Super Admin account
- [ ] Verified new account login works
- [ ] Deleted `gtadmin@test.com` account
- [ ] Enabled two-factor authentication
- [ ] Configured SMTP for email
- [ ] Activated Enterprise license
- [ ] Added at least one AI provider API key
- [ ] Updated tenant organization name

## Security Verification

After completing setup, verify security:

| Item | Check |
|------|-------|
| Default account removed | `gtadmin@test.com` not in Users list |
| TFA enabled | Settings shows TFA as enabled |
| SMTP working | Test email received |
| License active | License page shows your organization |

## Next Steps

Your Control Panel is now configured. Next:

- **Add Users**: Create accounts for your team in [User Management](user-management)
- **Configure Billing**: Set up pricing in [Financial Controls](financial-controls)
- **Test Tenant App**: Log in at http://localhost:3002 to verify chat works

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Can't log in after deleting default | See [Troubleshooting](troubleshooting) - database reset may be needed |
| TFA not working | Verify time sync on your authenticator device |
| SMTP test fails | Check spam folder, verify credentials, try App Password for Gmail |
| License won't activate | Ensure entire license string was copied, verify Deployment ID matches |
