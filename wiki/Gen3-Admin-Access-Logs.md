# Access Logs

## Start Here

1. Open **Access Logs**.
2. Filter by time range and actor for the incident window.
3. Correlate with tenant [Observability](gen3/observability) when investigating cross-plane issues.
4. Export or copy entries per compliance procedure.

## Why this matters

Access logs provide operator-plane audit evidence for security reviews and incident response.

## Details

`Access Logs` is the active Gen 3 Control Panel route for authentication and session-event review.

## What the page currently supports

- reviewing successful logins
- reviewing failed logins
- reviewing active sessions
- reviewing logout and timeout events
- filtering by user email
- filtering by event type
- filtering by platform
- filtering by start and end date
- exporting the current result set as CSV

## When to use Access Logs

Use this page when you need to answer questions like:

- Did a user actually sign in?
- Was the sign-in successful or rejected?
- Did a session time out?
- Was the event in the tenant app or the Control Panel?

## Recommended investigation workflow

1. Start with the broad time window.
2. Filter by user email if you know the account.
3. Narrow by event type or platform.
4. Export CSV if you need to hand the event set to another operator or audit process.

## Common scenarios

### Login troubleshooting

Filter to the user and the relevant date range, then compare successful and failed events before changing the user's account.

### Audit trail review

Use platform and time filters to isolate the specific environment or surface involved in the event review.

### Session timeout review

Filter for timeout events when users report unexpected sign-outs or when session policy changes are being evaluated.

## Best practices

- Filter before exporting so the CSV contains only the relevant event set.
- Check [Users](gen3-admin/users) only after the log evidence suggests an account-state change is needed.
- Revisit [Settings](gen3-admin/settings) when a pattern suggests the idle-timeout policy should be changed.

## Related pages

- [Users](gen3-admin/users)
- [Settings](gen3-admin/settings)
- [SSO Providers](gen3-admin/sso)
