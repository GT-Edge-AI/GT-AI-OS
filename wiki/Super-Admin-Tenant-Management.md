# Tenant Management

Manage your organization's tenants from the Tenants page. Tenants represent separate organizations or divisions within your GT AI OS deployment.

## Overview

A tenant is an isolated organization within GT AI OS. Each tenant has:

- Its own users and user permissions
- Separate agents and datasets
- Independent teams and conversations
- Isolated data storage

## Accessing Tenants

1. Click **Tenants** in the sidebar
2. The Tenants page displays all configured tenants

## Key Features

| Feature | Description |
|---------|-------------|
| Tenant List | View all tenants with status indicators |
| Edit Tenant | Modify tenant settings and configuration |
| Deploy Tenant | Activate pending tenants |
| License Status | See seat usage per tenant |

## Tenant List

The Tenants page shows:

| Column | Description |
|--------|-------------|
| **Name** | Organization/tenant name |
| **Domain** | Unique identifier for the tenant |
| **Status** | Active, Pending, or Disabled |
| **Users** | Number of users in this tenant |
| **Actions** | Edit and manage options |

### Status Indicators

| Status | Meaning |
|--------|---------|
| **Active** | Tenant is fully operational |
| **Pending** | Tenant created but not deployed |
| **Disabled** | Tenant is deactivated |

## How To: Edit a Tenant

Modify tenant settings:

1. Navigate to **Tenants** page
2. Find the tenant you want to edit
3. Click the **Edit** button (pencil icon)
4. Update the fields:
   - **Name:** Organization display name
   - **Domain:** Unique identifier (cannot be changed after creation)
   - **Frontend URL:** URL where users access the Tenant App
   - **Status:** Enable or disable the tenant
5. Click **Save**

## How To: Deploy a Pending Tenant

When a new tenant is created, it may be in "Pending" status until deployed:

1. Navigate to **Tenants** page
2. Find tenants with **Pending** status
3. Click the **Deploy** button
4. Wait for deployment to complete
5. Status changes to **Active**

Deployment provisions the tenant's database schema and initializes resources.

## Tenant Settings

Each tenant can be configured with:

| Setting | Description |
|---------|-------------|
| **Name** | Display name shown to users |
| **Domain** | Internal identifier, used in URLs and database |
| **Frontend URL** | Where the Tenant App is accessed |
| **Description** | Optional notes about the tenant |

## License and Seat Management

Each active user across all tenants consumes one license seat.

| View | Where |
|------|-------|
| Total seats used | License page |
| Per-tenant users | Tenants page (Users column) |
| User details | Users page (filter by tenant) |

### Managing Seat Usage

If you're approaching your seat limit:

1. Review users across all tenants
2. Disable inactive users to free seats
3. Contact GT Edge AI for additional seats

## Default Tenant

Fresh installations include one default tenant:

- **Name:** GT AI OS (or Test Company)
- **Domain:** test-company (or similar)
- **URL:** http://localhost:3002

You should update this tenant to match your organization:

1. Edit the default tenant
2. Change **Name** to your organization name
3. Update **Frontend URL** if using a custom domain
4. Save changes

## Multi-Tenant Considerations

When running multiple tenants:

| Consideration | Best Practice |
|---------------|---------------|
| Data isolation | Each tenant's data is isolated by database schema |
| User accounts | Users can belong to one tenant only |
| Shared resources | AI models are configured globally, available to all tenants |
| License seats | Counted across all tenants |

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Tenant stuck in Pending | Check database connectivity, view backend logs |
| Can't edit tenant | Verify Super Admin permissions |
| Users can't access | Verify tenant status is Active |
| Domain conflict | Each tenant must have a unique domain |

### Checking Tenant Status

If a tenant isn't working:

```bash
# Check backend logs
docker compose logs control-panel-backend --tail 100

# Check tenant database schema exists
docker exec gentwo-tenant-postgres psql -U gt2_tenant_user -d gt2_tenants -c "\dn"
```

## Next Steps

- [User Management](user-management) - Add users to your tenants
- [License Management](license-management) - Monitor seat usage
- [Financial Controls](financial-controls) - Configure tenant billing
