# SSO Providers

## Start Here

1. Open **SSO Providers**.
2. Create or edit the identity provider mapping for this deployment.
3. Test sign-in with a low-risk operator account.
4. Document issuer and redirect URLs for your IdP team.

## Why this matters

SSO misconfiguration blocks all operator access; validate before broad rollout.

## Details

`SSO Providers` is the active Gen 3 Control Panel workspace for upstream identity integration. It manages OIDC and SAML provider configuration, claim mapping, validation, and provisioning behavior from one page.

## What the page currently supports

- creating upstream OIDC or SAML providers
- editing provider runtime details
- enabling or disabling providers
- validating provider configuration
- reviewing broker runtime URLs
- configuring provisioning policy
- reviewing or rotating write-only secrets by replacing values intentionally
- deleting providers that are no longer needed

## Supported provider shapes

### OIDC

Use OIDC when your identity provider can expose issuer or discovery metadata plus the client credentials needed for brokered sign-in.

### SAML

Use SAML when the identity provider publishes SAML metadata URL or entity details instead of OIDC discovery.

## Provisioning controls

The provisioning workflow lets you define how accounts should be created and updated after sign-in, including role posture and deprovision behavior. Review this carefully before enabling a provider in production.

## Recommended rollout workflow

1. Create the provider in `SSO Providers`.
2. Enter the required OIDC or SAML details.
3. Save the configuration.
4. Run validation from the provider row.
5. Review provisioning settings.
6. Enable the provider only after validation succeeds.

## Operational cautions

- Client secrets and SCIM bearer tokens are write-only. Leaving those fields blank keeps the current value.
- A bad SSO change can affect both Control Panel and tenant access, so validate before broad rollout.
- Delete only after confirming the deployment no longer depends on the provider.

## Best practices

- Keep one clear owner for each upstream provider.
- Validate before and after major edits.
- Document which audience each provider serves.
- Review provisioning defaults so new users land with the intended role posture.

## Related pages

- [Users](gen3-admin/users)
- [Access Logs](gen3-admin/access-logs)
- [Settings](gen3-admin/settings)
