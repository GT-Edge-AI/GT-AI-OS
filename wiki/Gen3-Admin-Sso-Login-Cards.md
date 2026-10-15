# Login Cards

## Start Here

1. Open **SSO Providers** and edit the provider people should see at sign-in.
2. Leave **Show description on the login card** checked to show a sentence, or clear it to hide the sentence.
3. In **Login card description**, type the sentence visitors should read, or leave it blank to keep the default sentence for that protocol.
4. Save the provider.
5. Open the tenant login page and the Control Panel login page in a private window and confirm the card.

## Why this matters

When SSO is configured, both login pages lead with those providers. The sentence on each card is the short guidance next to the provider name. You can show it, hide it, or replace it without removing the protocol badge people use to tell OIDC and SAML apart.

## Details

### What visitors see

Configured SSO providers are listed first on Control Panel login and tenant login. Each card keeps the **OIDC** or **SAML** badge on the right. The badge cannot be turned off. The card action is **Continue with SSO**.

Under the cards, a box reads **Sign in with email and password**, with the hint **Use your GT AI OS account**. Choosing that box opens the username and password form.

When no SSO provider is configured, that username and password form is open immediately. After a password reset, an account-linking notice, or a credential error, the form also opens so the visitor can read the notice.

### Edit the sentence

On the provider form:

| Control | Effect |
| --- | --- |
| **Show description on the login card** | Checked shows the sentence. Cleared hides it. The protocol badge stays. |
| **Login card description** | Up to 240 characters. Blank uses the default sentence for OIDC or SAML. The field is unavailable while the sentence is hidden. |

The form states: the OIDC or SAML badge stays on the right of every login card so people can see which protocol they are using. That badge cannot be hidden.

Save, then sign in once as a low-risk account before you announce the change. A stale hosted SSO session restarts sign-in instead of stopping on the branded server-error page. See [SSO Providers](gen3-admin/sso).

## Related pages

- [SSO Providers](gen3-admin/sso)
- [Users](gen3-admin/users)
- [Access Logs](gen3-admin/access-logs)
