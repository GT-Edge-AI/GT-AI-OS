# License Management

View your deployment ID, activate licenses, and manage seat allocations from the License page.

## Overview

GT AI OS Enterprise uses deployment-specific licensing:

- **Deployment ID:** Unique identifier for your installation
- **Seat-based:** Licenses specify maximum active users
- **Cryptographically signed:** Cannot be modified or transferred

## Accessing License Management

1. Click **License** in the sidebar
2. The page displays your deployment ID and license status

## Key Features

| Feature | Description |
|---------|-------------|
| Deployment ID | Your unique installation identifier |
| License Activation | Paste and activate license |
| License Status | View seats, expiration, type |
| Seat Tracking | Monitor usage vs allocation |

## License Page Sections

### Deployment ID

Your unique installation identifier:

1. Find the **Deployment ID** card
2. Click **Show** to reveal the full ID
3. Click **Copy** to copy to clipboard

Format: `gt2-550e8400-e29b-41d4-a716-446655440000`

**Important:** The Deployment ID is generated on first access and remains constant for your installation.

### License Status

After activation, displays:

| Field | Description |
|-------|-------------|
| **Max Seats** | Maximum active users allowed |
| **Used Seats** | Current active user count |
| **Valid Until** | License expiration date |
| **Status** | Active, Expired, or Trial |
| **License Type** | Enterprise, Trial, etc. |

### License Activation

Area to paste and activate your license:

1. Paste license string in textarea
2. Click **Activate License**
3. Wait for validation
4. View updated status

## How To: Get Your Deployment ID

1. Navigate to **License** page
2. Find the **Deployment ID** section
3. Click **Show** to reveal the ID
4. Click **Copy** to copy
5. Send to GT Edge AI support to receive your license

## How To: Activate a License

Once you receive your license from GT:

1. Navigate to **License** page
2. Find the **License Activation** section
3. Paste the entire license content into the textarea
4. Click **Activate License**
5. Wait for validation (signature verification)
6. View your license details

### License Format

Valid licenses look like:
```
LIC-ABC123DEF456:jYuxwFtJbrmn20k/uoMYKj...
```

- Starts with `LIC-`
- Contains a colon `:`
- Followed by encrypted data

## Understanding Your License

### Seat Management

Each active user consumes one seat:

| User Status | Seat Usage |
|-------------|------------|
| Active | Uses 1 seat |
| Disabled | No seat used |
| Deleted | No seat used |

### When Seats Are Full

If you reach your seat limit:

- New user creation is blocked
- Existing users continue working
- Message indicates seat limit reached

### Freeing Seats

To create more users when at limit:

1. Navigate to **Users** page
2. Find inactive users
3. **Disable** or **Delete** unused accounts
4. Seats become available immediately

## License States

| State | Meaning |
|-------|---------|
| **Not Activated** | No license applied, limited users |
| **Active** | License valid and working |
| **Expired** | License past expiration date |
| **Invalid** | License doesn't match deployment |

### Expired Licenses

When a license expires:

- Existing users continue working
- New user creation may be blocked
- Contact GT for renewal license

### Renewal Process

1. Contact GT Edge AI support
2. Request renewal license
3. Receive new license string
4. Activate using same process
5. New expiration date applies

## License Security

### What's Protected

| Feature | Protection |
|---------|------------|
| Deployment binding | License tied to specific Deployment ID |
| Cryptographic signature | Cannot be modified |
| Expiration enforcement | System validates date |

### What Happens If

| Scenario | Result |
|----------|--------|
| License modified | Activation fails, signature invalid |
| Different deployment | Activation fails, ID mismatch |
| Database reset | New Deployment ID generated, need new license |
| License shared | Only works on original deployment |

## Deployment ID Changes

The Deployment ID may change if:

- Database is completely reset (`docker compose down -v`)
- Fresh installation is performed
- System is migrated to new hardware

If your Deployment ID changes:

1. Copy the new Deployment ID
2. Contact GT Edge AI support
3. Request license re-issue
4. Activate the new license

## Troubleshooting

### "License activation failed"

| Cause | Solution |
|-------|----------|
| Incomplete license | Copy the entire string including `LIC-` prefix |
| Wrong Deployment ID | License was generated for different installation |
| Corrupted license | Request new license from GT |
| Expired license | Request renewal license |

### "Cannot create more users"

- You've reached your seat limit
- Solution: Disable unused accounts or upgrade license

### "Deployment ID not showing"

- Refresh the page
- Check database connectivity
- View backend logs for errors

### "License shows different organization"

- This shouldn't happen with valid licenses
- Contact support to verify license details

### Checking License Status

```bash
# View license-related logs
docker compose logs control-panel-backend --tail 100 | grep -i license

# Check license in database
docker exec gentwo-controlpanel-postgres psql -U postgres -d gt2_admin -c "SELECT * FROM licenses;"
```

## Without a License

Without an activated license:

| Feature | Status |
|---------|--------|
| User creation | Limited to trial count |
| All features | Available |
| Enterprise support | Not included |

## Getting a License

1. **Copy Deployment ID** from License page
2. **Contact GT Edge AI** with your Deployment ID
3. **Provide details:**
   - Organization name
   - Number of users needed
   - Contract/purchase order reference
4. **Receive license** via email
5. **Activate** using steps above

## Next Steps

- [User Management](user-management) - Manage users within seat allocation
- [Deployment Checklist](deployment-checklist) - Complete initial setup
- [Troubleshooting](troubleshooting) - Resolve license issues
