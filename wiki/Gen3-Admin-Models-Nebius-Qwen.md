# Nebius and Qwen

## Start Here

1. Open **Models** → **Inference Providers**.
2. Create or edit the OpenAI-compatible provider for Nebius Token Factory.
3. Set the base URL to `https://api.tokenfactory.us-central1.nebius.com/v1/`.
4. Save the provider, then use **Quick Add** or model discovery to import the Qwen models you need.
5. Send a dataset-backed chat that includes retrieval guidance and confirm the call succeeds.

## Why this matters

Qwen on Nebius Token Factory rejects a system message that appears after a user or assistant turn. GT AI OS sends every system message as one message at the start of the request, so dataset guidance and evidence checks stay in that leading message.

## Details

This merge applies to Nebius Token Factory and to any Qwen model on an OpenAI-compatible provider. Other providers keep mid-conversation system turns unless the inference policy `mergeSystemMessages` is set for that provider.

Point the provider base URL at `https://api.tokenfactory.us-central1.nebius.com/v1/` on this release. The product performs the merge before the request leaves the cluster. You do not put the proxy in front of Nebius for a current interim build.

### When an older build still needs a proxy

`gt-ai-os/scripts/nebius-system-message-proxy` (`proxy.py`) is for a release that does not yet merge system messages itself. Run it on a host the cluster can reach. It is Python standard library only.

| Environment variable | Purpose | Default |
| --- | --- | --- |
| `LISTEN` | Address the proxy binds | `0.0.0.0:19000` |
| `NEBIUS_UPSTREAM` | Nebius host the proxy forwards to | `https://api.tokenfactory.us-central1.nebius.com` |

The proxy joins every system message into one message at the start, then forwards the request. It passes `Authorization` through and does not store an API key. On that older layout, set the GT AI OS provider base URL to the proxy, and let the proxy forward to Nebius.

On the current interim, skip the proxy and use the Nebius base URL directly.

### Quick Add on a Tailscale or CGNAT address

If the provider base URL is in `100.64.0.0/10`, **Quick Add** states that this is a Tailscale/CGNAT address. Discovery runs from GT AI OS cluster pods, not your browser. Each cluster node needs a route to that host (for example via a VLAN Tailscale exit node). Model discovery uses the local-inference ports from those pods.

## Related pages

- [Models](gen3-admin/models)
- [Model Capabilities](gen3-admin/models/capabilities)
