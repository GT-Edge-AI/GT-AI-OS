# Troubleshooting

Find solutions to common Control Panel issues. For general GT AI OS problems, see the main Troubleshooting documentation.

## Overview

This guide covers:

- Login and authentication issues
- User management problems
- SMTP and email issues
- License activation problems
- Common error messages

## Authentication Issues

### "I forgot the login password"

**Default credentials:**
- Email: `gtadmin@test.com`
- Password: `Test@123`

**If you changed the password:**

With SMTP configured:
1. Click "Forgot Password?" on login page
2. Enter your email
3. Check inbox for reset link
4. Set new password

Without SMTP:
- You'll need database access or a full reset

### "I can't log in after deleting the default admin"

You deleted `gtadmin@test.com` before verifying your new account works.

**Solution:**

1. Navigate to your GT AI OS folder:
   ```bash
   cd ~/Desktop/GT-2.0   # Mac
   cd ~/GT-2.0           # Ubuntu/DGX
   ```
2. Reset the database:
   ```bash
   docker compose down -v
   docker compose up -d
   ```
3. Wait 2-3 minutes
4. Login with: `gtadmin@test.com` / `Test@123`
5. **This time:** Verify new account works BEFORE deleting default

### "I'm locked out due to TFA"

You lost access to your authenticator app.

**Option 1: Admin TFA Reset**

If another admin has access:
1. Have them reset your TFA from Users page
2. Log in without TFA
3. Set up TFA again

**Option 2: Command Line Reset**

```bash
# Reset TFA for all users
cd ~/Desktop/GT-2.0 && ./scripts/recovery/reset-tfa.sh

# Or via SQL
docker exec gentwo-controlpanel-postgres psql -U postgres -d gt2_admin -c "UPDATE users SET tfa_enabled = false, tfa_secret = NULL WHERE tfa_enabled = true;"
```

**Option 3: Full Reset**
- See "Database Reset" section below

### "Session expired unexpectedly"

GT AI OS uses NIST-compliant session timeouts:

| Timeout | Duration | Behavior |
|---------|----------|----------|
| Idle | 30 minutes | Resets with activity |
| Absolute | 12 hours | Cannot be extended |

This is by design for security. Log in again when sessions expire.

## User Management Issues

### "Cannot create more users"

You've reached your license seat limit.

**Solutions:**
1. Go to **Users** page
2. Find and disable inactive users
3. Or contact GT for license upgrade

### "Email already in use"

Each email must be unique across all tenants.

**Solutions:**
- Use a different email address
- Find and remove duplicate user first

### "User can't access Control Panel"

Only Super Admin users can access the Control Panel.

**Check:**
1. Go to **Users** page
2. Find the user
3. Verify **User Type** is "Super Admin"
4. If not, edit and change user type

### "User not receiving welcome email"

| Check | Solution |
|-------|----------|
| SMTP configured? | Test SMTP first |
| Welcome emails enabled? | Check Email Settings |
| Valid email address? | Verify email format |
| Spam folder? | Check junk/spam |

## Email Issues

### "Test email not received"

1. **Check spam folder** - Test emails often filtered
2. **Verify SMTP credentials** - Username and password correct
3. **Check from address** - Must be authorized for your SMTP server
4. **Try different recipient** - Test with another email

### "Authentication failed" for SMTP

| Provider | Solution |
|----------|----------|
| Gmail | Use App Password from https://myaccount.google.com/apppasswords |
| Office 365 | Enable "Authenticated SMTP" in admin portal |
| Others | Verify username is full email address |

### "Connection failed" for SMTP

| Check | Solution |
|-------|----------|
| Host correct? | Double-check SMTP host address |
| Port correct? | Try 587 (TLS) or 465 (SSL) |
| Firewall? | Ensure outbound port is open |
| TLS setting? | Toggle "Use TLS" option |

### "Password reset email not sent"

1. SMTP must be configured and tested first
2. User must exist and be active
3. Check rate limit (5 requests per email per hour)
4. Verify correct email address entered

## License Issues

### "License activation failed"

| Cause | Solution |
|-------|----------|
| Incomplete content | Copy entire license string (starts with `LIC-`) |
| Wrong Deployment ID | License was generated for different installation |
| Corrupted | Request new license from GT |
| Expired | Request renewal license |

### "Deployment ID changed"

If your Deployment ID changed (database reset, new installation):

1. Copy new Deployment ID from License page
2. Contact GT Edge AI support
3. Request license re-issue for new ID
4. Activate the new license

### "License shows expired"

Contact GT Edge AI support for a renewal license.

## Model and API Issues

### "API key test fails"

**For NVIDIA:**
- Copy complete key
- Verify at https://build.nvidia.com/

**For Groq:**
- Key should start with `gsk_`
- Verify at https://console.groq.com/

**General:**
- No extra spaces in key
- Try generating new key

### "Models not appearing"

1. Verify API key is configured and tested
2. Check correct provider for model type
3. Refresh page (F5)
4. Restart backend:
   ```bash
   docker compose restart control-panel-backend
   ```

## Database Reset

**Warning:** This deletes ALL data including users, settings, and licenses.

Use only when all other options exhausted:

1. Navigate to GT AI OS folder:
   ```bash
   cd ~/Desktop/GT-2.0   # Mac
   cd ~/GT-2.0           # Ubuntu/DGX
   ```

2. Stop and remove everything:
   ```bash
   docker compose down -v
   ```

3. Start fresh:
   ```bash
   docker compose up -d
   ```

4. Wait 2-3 minutes
5. Login with default: `gtadmin@test.com` / `Test@123`
6. Complete [Deployment Checklist](deployment-checklist) again

## Debugging

### View Logs

```bash
# All services
docker compose logs -f

# Control Panel backend only
docker compose logs -f control-panel-backend

# Last 100 lines
docker compose logs control-panel-backend --tail 100
```

### Search Logs

```bash
# SMTP issues
docker compose logs control-panel-backend | grep -i smtp

# Authentication issues
docker compose logs control-panel-backend | grep -i auth

# License issues
docker compose logs control-panel-backend | grep -i license
```

### Check Container Status

```bash
# All containers
docker compose ps

# Specific service health
docker inspect gentwo-control-panel-backend --format='{{.State.Health.Status}}'
```

### Database Queries

```bash
# Check users
docker exec gentwo-controlpanel-postgres psql -U postgres -d gt2_admin -c "SELECT email, user_type, is_active FROM users;"

# Check license
docker exec gentwo-controlpanel-postgres psql -U postgres -d gt2_admin -c "SELECT * FROM licenses;"

# Check SMTP config (without password)
docker exec gentwo-controlpanel-postgres psql -U postgres -d gt2_admin -c "SELECT smtp_host, smtp_port, smtp_username FROM smtp_configs;"
```

## Quick Reference

| Symptom | First Try |
|---------|-----------|
| Can't login | Check credentials, try default |
| Forgot password | Use "Forgot Password?" (needs SMTP) |
| TFA locked | Reset TFA via command line |
| Can't create users | Check license seats |
| Email not sending | Test SMTP configuration |
| License won't activate | Verify complete string copied |
| Models missing | Check API key configuration |

## Getting More Help

### Check Logs First

Most issues are visible in logs:
```bash
docker compose logs control-panel-backend --tail 200
```

### Open Support Ticket

Contact GT Edge AI support with:
1. Description of the issue
2. Steps to reproduce
3. Error messages (from logs)
4. Deployment ID (from License page)

### GitHub Issues

For bug reports and feature requests:
https://github.com/GT-Edge-AI/GT-AI-OS/issues

Include:
- GT AI OS version
- Platform (Mac, Ubuntu, DGX)
- Relevant log output
- Steps to reproduce
