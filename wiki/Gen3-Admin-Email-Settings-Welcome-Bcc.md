# Welcome Email BCC

## Start Here

1. Open **Email Settings** and select **Welcome Email**.
2. Check **BCC a logging or archive address on welcome emails**.
3. Under **BCC recipients**, enter the archive mailbox and click **Add BCC**.
4. Click **Save welcome policy**.
5. Onboard a test user and confirm the archive mailbox receives a copy that is absent from the recipient’s To and CC lines.

## Why this matters

A logging or archive mailbox can keep a copy of onboarding mail without appearing to the new user. The copy is hidden from To and CC.

## Details

The control sits on the welcome policy card, next to welcome delivery and CC options. The note under the checkbox reads: hidden from the new user. Use this for a mail-archive or logging mailbox that should receive a copy without appearing in To or CC.

**BCC recipients** stays disabled until the checkbox is on. Add one address at a time. The placeholder example is `archive@example.com`. Remove an address with the control on its token. When the list is empty, the page says **No BCC recipients configured.**

This list is separate from **Additional CC recipients**, **CC super administrators**, and **CC environment administrators**. CC addresses can be visible to the recipient. BCC addresses are the hidden copies.

Welcome mail still has to be enabled. **Send welcome emails for eligible onboarding flows** and **Send Tenant App welcome emails** control whether a message is sent at all. SMTP has to be working before a BCC copy can arrive. See [Email Settings](gen3-admin/email-settings).

## Related pages

- [Email Settings](gen3-admin/email-settings)
- [Email Templates & Modules](gen3-admin/email-templates)
