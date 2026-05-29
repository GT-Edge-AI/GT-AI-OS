# Managing Membership and Sharing

## Start Here

1. Open **Groups** and select the group to administer.
2. Review current members and pending invitations.
3. Add or remove members according to tenant policy.
4. Audit shared agents and datasets after membership changes.

## Why this matters

Membership changes are a security and data-isolation event—stale members should not retain access to shared resources.

## Details

The detailed group management shelf is where Gen 3 handles membership, invitations, observable requests, and resource sharing for a specific group. Use it after you select a group from the main [Groups](gen3/groups) page.

## The three active shelf areas

### Overview

The overview tab shows the group's role posture, default resource permission, member counts, managed-group governance fields, and pending observable requests for managers.

### Members

The members tab is where you:

- invite users by email
- bulk add users from a pasted list
- review current members and pending invitations
- adjust group permission levels
- request or review observable access
- update tenant role from the group member roster when your permissions allow it

### Resources

The resources tab is where you share or unshare:

- agents
- datasets

Shared resources inherit the group's permission model, so membership and resource sharing should be reviewed together rather than as separate workflows.

## Common tasks

### Invite a user

1. Open the group management shelf.
2. Move to `Members`.
3. Enter the user's email.
4. Choose the group permission level.
5. Send the invitation.

### Bulk add members

Use the bulk-add path when you already have a prepared list of addresses. This is faster than repeating single invites and keeps the group rollout consistent.

### Share an agent or dataset

1. Open the group management shelf.
2. Move to `Resources`.
3. Choose the agent or dataset to share.
4. Confirm the share.
5. Verify that the members who need the resource can now see it.

## Permission model

The current group workflow distinguishes between group permission levels such as read, share, and manager. Give users the minimum level that still matches their responsibility.

## Observable requests

Managed groups can surface observable requests so a group manager can approve or deny deeper visibility. Review these from the overview area before assuming observability data is missing.

## Best practices

- Keep membership aligned to the smallest real collaboration audience.
- Review resource sharing after large membership changes.
- Use managed groups when you need a real manager approval path.
- Avoid using groups as a substitute for tenant-wide visibility when the content is actually global.

## Related pages

- [Groups](gen3/groups)
- [Sharing Agents](gen3/agents/sharing)
- [Datasets](gen3/datasets)
