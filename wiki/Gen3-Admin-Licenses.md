# License

## Start Here

1. Open **License**.
2. Review entitlement status and expiration.
3. Apply updated license material when sales operations provides it.
4. Validate tenant access after renewal.

## Why this matters

License state gates product availability—operators should verify renewal before users interpret errors as application bugs.

## Details

`License` is the active Gen 3 Control Panel route for enterprise license review and activation.

## What the page currently shows

The live page includes:

- current license information
- license type and status
- seat usage
- expiry posture
- deployment identifier details
- license activation workflow

## Common tasks

### Confirm current license posture

Review the license-information card to check whether the deployment is active, in a trial posture, or needs attention.

### Review deployment identity

Use the deployment-information area when you need the deployment identifier associated with this GT AI OS instance. This is especially important during activation or renewal workflows.

### Activate or replace a license

The page supports both upload and paste-style activation. Use the activation workflow when applying a new license string or file to the deployment.

## Recommended activation workflow

1. Open `License`.
2. Confirm the deployment identifier.
3. Upload or paste the license payload.
4. Run activation.
5. Re-check status, seat posture, and expiry.

## When to use this page vs other billing pages

- Use `License` for license activation and status.
- Use [Financial Controls](gen3-admin/financial-controls) for billing and pricing policy.

## Best practices

- Verify the deployment identifier before activation.
- Re-check seat usage after a new license is applied.
- Treat activation issues as a license or deployment-identity problem first, not as a billing-policy problem.

## Related pages

- [Dashboard](gen3-admin/dashboard)
- [Financial Controls](gen3-admin/financial-controls)
