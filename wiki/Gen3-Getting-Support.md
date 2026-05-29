# Support

## Start Here

1. Open **Contact support** from the tenant sidebar footer user menu (or the support links shown on sign-in when enabled).
2. Review published support email and portal links (sourced from Control Panel policy).
3. Use in-app report actions on chat messages when you need prompt/response evidence.
4. Gather conversation id, agent name, and timestamp before contacting support.

## Why this matters

Support routes connect tenant users to operator-published contacts and structured reporting so incidents are actionable without exposing internal operator tools.

## Details

Gen 3 exposes support through the tenant shell instead of a separate administrative page. In the active tenant product there are two support entry points: the **Instructions** menu and the **Contact support** menu.

## Instructions menu

The instructions menu is the in-product help entry point. Depending on deployment settings, it can expose:

1. **GT AI OS Instructions** to open the built-in wiki drawer
2. **Operator documentation** when the deployment publishes an operator-managed docs URL
3. **External instructions** when Control Panel operators enable an additional external link

Use the instructions drawer for workflow guidance, page explanations, and step-by-step product help.

## Contact support menu

The Contact support menu is published from the Control Panel email/support policy. It can expose:

- an email-only contact path
- a support portal URL
- both options together

If you do not see Contact support, the deployment has not published a support policy for tenant users.

## When to use each support path

| Need | Best path |
| --- | --- |
| Learn how a page or workflow works | Open **Instructions** |
| Conversational in-app help on the current screen | [GT Helper](gen3/agents/helper-agent) — **?** help shelf |
| Reach an operator or help desk | Open **Contact support** |
| Report a bad chat response or runtime issue | Use the in-chat **Report** action, then send the report through your support path |
| Confirm tenant policy or recovery posture | Review [Account Settings](gen3/settings) |

## Reporting a chat issue

Assistant-message actions in GT Chat include **Report** when a completed assistant response is available. Use it when you need to capture the current message plus the prompt that led to it.

Recommended flow:

1. Open the affected conversation in [GT Chat](gen3/chat).
2. Locate the assistant response that demonstrates the problem.
3. Select **Report** from the message actions.
4. Review the generated report details.
5. Share the resulting material through the deployment's support email or portal.

## Common support scenarios

### I cannot sign in

- Confirm that you are using the correct tenant login page and email address.
- Use the password reset path if your deployment allows password-reset email.
- If access is still blocked, contact a tenant owner or tenant manager through the published support path.

### I cannot find an agent or dataset

- Check [Agents](gen3/agents) and [Datasets](gen3/datasets) directly.
- Confirm whether the resource is private, group-shared, or organization-visible.
- If the resource should have been shared to you, ask the owner or the relevant group manager to confirm visibility.

### I cannot see a page another user sees

Page visibility in Gen 3 depends on your role. Tenant user administration is limited to [Users](gen3/users) for tenant owners and tenant managers, and observability scope also changes by role.

### Contact support is missing

The support menu is driven by Control Panel email settings. If it is absent, your deployment has not published a valid support email, a support portal URL, or both.

## Related pages

- [GT Helper](gen3/agents/helper-agent)
- [GT Chat](gen3/chat)
- [Conversations](gen3/conversations)
- [Account Settings](gen3/settings)
- [Users](gen3/users)
