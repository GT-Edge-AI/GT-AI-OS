# Observability (Tenant Admin)

This section covers Tenant Admin-specific Observability features. For general usage (viewing your own activity, conversations, and storage), see [Observability](observability).

## Admin-Only Features

As a Tenant Admin, you have access to additional Observability features:

| Feature | Description |
|---------|-------------|
| Organization-wide view | See all users' activity, not just your own |
| User filtering | Filter any data by specific users |
| Access Logs | View login history and authentication events |
| Billing | Track costs and credit consumption (if enabled) |

## Organization-Wide Monitoring

### Viewing All Activity

Unlike regular users who only see their own data, Tenant Admins see:
- All conversations across the organization
- Usage metrics for all users
- Storage consumption by all users and datasets

### Filtering by User

On the Usage Overview, Conversations, and Storage tabs, you can:
1. Use the **User** dropdown to select specific users
2. View activity for individual users or the entire organization
3. Compare usage patterns across users

## Access Logs

The Access Logs tab (admin-only) shows authentication and access events.

### What You Can See

- **Login events**: When users logged in
- **Logout events**: When users logged out
- **Failed attempts**: Failed login attempts
- **IP addresses**: Where logins originated from
- **Timestamps**: When each event occurred

### Using Access Logs

1. Go to **Observability**
2. Click the **Access Logs** tab
3. Filter by:
   - Date range
   - Specific users
   - Event type (login, logout, failed)
4. Review events for security monitoring

### Security Monitoring

Use access logs to:
- Detect unusual login patterns
- Identify failed login attempts
- Verify user activity
- Support security investigations

## Billing

The Billing tab (admin-only) shows cost and credit information. This tab only appears if billing is enabled for your tenant.

### Cost Overview

View costs broken down by:
- Total organization spend
- Per-user costs
- Per-agent costs
- Storage costs
- Inference costs

### Credit Tracking

Monitor credit consumption:
- Current balance
- Usage trends
- Per-user breakdown
- Projected usage

### Billing Reports

Export billing data for:
- Finance reporting
- Budget planning
- Cost allocation
- Usage audits

## Privacy Considerations

When accessing other users' data:
- Follow your organization's privacy policies
- Only access data when necessary for your role
- Document reasons for accessing user conversations
- Respect user privacy expectations
- Be aware that your access may be logged

## Best Practices

### Regular Monitoring

Establish a routine:
- **Daily**: Quick check of activity and access logs
- **Weekly**: Review usage trends and anomalies
- **Monthly**: Comprehensive analysis and reporting
- **Quarterly**: Strategic review and planning

### Investigating Issues

When users report problems:
1. Use user filtering to find their conversations
2. Review the relevant interactions
3. Check access logs if authentication issues are suspected
4. Take appropriate action

### Evaluating Platform Usage

Use organization-wide data to:
- Identify popular agents
- Find underutilized resources
- Spot training opportunities
- Plan capacity and budgets

## Troubleshooting

### Access Logs Not Loading

1. Verify you have Tenant Admin role
2. Check your date range selection
3. Try refreshing the page
4. Contact support if issues persist

### Billing Tab Not Visible

The Billing tab only appears if:
- Billing is enabled for your tenant
- You have Tenant Admin role

Contact your Super Admin if you believe billing should be enabled.
