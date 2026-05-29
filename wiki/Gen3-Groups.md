# Groups

## Start Here

1. Open **Groups** from the tenant sidebar.
2. Create or join a group per collaboration boundary.
3. Invite members and confirm roles.
4. Share agents and datasets into the group when resources should move with membership.

## Why this matters

Groups align sharing with real teams so agents and datasets do not leak tenant-wide when only a unit should collaborate.

## Details

Gen 3 uses **Groups** as the active collaboration boundary where GT2 often exposed similar behavior under teams. Groups control who collaborates together and which shared agents or datasets are visible inside that collaboration space.

## What the current page supports

The active `Groups` page supports:

- creating groups
- editing group details
- reviewing pending invitations
- reviewing pending observable requests
- searching and filtering the group list
- leaving groups you do not own
- deleting groups you own
- opening the detailed group management shelf

## Open collaboration vs managed groups

Gen 3 supports two collaboration styles:

- **Open collaboration groups** for general shared work
- **Managed groups** with an assigned manager and governance fields such as monthly budget, budget notes, allowed model IDs, and default spend scope

If a group is managed, expect stronger controls around observability and administration.

## Main page workflow

1. Open `Groups`.
2. Review any pending invitations or observable requests.
3. Use search, membership filters, and sorting to find the group you want.
4. Open the group's management shelf for detailed actions.

## What you can do from the list page

### Create a group

The create form supports the group name, description, default resource permission, and optional managed-group governance fields. Use managed groups when a group needs an explicit manager or policy controls rather than lightweight collaboration.

### Review invitations and observable requests

The active GT3 page surfaces invitation banners and observable-request banners directly on the route. Handle those before troubleshooting missing group access.

### Bulk leave or delete

The list supports selection-based leave and delete actions where your permissions allow them. Owners can delete owned groups, while non-owners can leave groups they no longer need.

## How groups affect other pages

- [Agents](gen3/agents/sharing) can be shared into a group
- [Datasets](gen3/datasets) can be group-shared
- [Observability](gen3/observability) may use managed-group scope for some tenant managers

## Best practices

- Create separate groups when membership or resource access genuinely differs.
- Use clear names and descriptions so users know why a group exists before joining it.
- Prefer group sharing over broad organization-wide visibility when content is team-specific.
- Use managed groups when you need explicit oversight, model restrictions, or budget notes.

## Related guidance

- [Managing Membership and Sharing](gen3/groups/managing-membership)
- [Sharing Agents](gen3/agents/sharing)
- [Datasets](gen3/datasets)
