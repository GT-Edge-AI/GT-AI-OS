# API Addresses

## Start Here

1. Confirm GT API is enabled for your tenant. The **GT API** sidebar item is hidden when it is off.
2. Open **GT API** (`/gt-api`).
3. At the top, read **API address**.
4. Click **Copy** next to **FQDN** or **Base URL**, or **Copy** on one endpoint row.
5. Click **Copy all** when you want the FQDN, base URL, and every endpoint URL in one block.

## Why this matters

Integrators need the live host and full URLs for this tenant, not a placeholder. The panel is built from the site you are signed into, so the values match the tenant app you have open.

## Details

**API address** sits above **API Keys** and **Published Endpoints**. The description reads: copy the FQDN or base URL into external apps. Each endpoint URL is that base URL plus the route.

| Field | What to paste |
| --- | --- |
| **FQDN** | The host (and port, if the site uses one) of this tenant. |
| **Base URL** | `https://<that-host>/api/tenant` |

The **Endpoint URLs** table lists method, use, and the full URL. Each row has its own **Copy** button. **Copy all** produces:

```text
FQDN: <host>
Base URL: <origin>/api/tenant

GET <origin>/api/tenant/v1/models
POST <origin>/api/tenant/v1/chat/completions
```

The table includes list models, chat completion, embeddings, transcribe audio, speech, generate an image, create a GT conversation, list upload targets, upload a file to a dataset alias, upload a file to a conversation, file processing status, and upload status. Dataset and file rows keep `{datasetId}`, `{fileId}`, or `{uploadId}` in the path so you can substitute the alias or id your key is allowed to use.

A copied URL is not a credential. Callers still need a bearer key and a published alias. See [API Keys and Access](gen3/gt-api/keys-and-access) and [Published Endpoints](gen3/gt-api/published-endpoints).

While the page is still reading the site address, the panel says **Reading this site’s address.** Wait for **FQDN** and **Base URL** before you copy.

## Related pages

- [GT API Overview](gen3/gt-api/overview)
- [API Keys and Access](gen3/gt-api/keys-and-access)
- [Published Endpoints](gen3/gt-api/published-endpoints)
- [OpenAI SDK / curl](gen3/gt-api/runbooks/openai-sdk-curl)
