# Group Managers

## Start Here

1. Open **Groups**. Tenant owners and tenant managers can assign managers. Tenant users can open a group and review it.
2. Choose **New group**, or open an existing group and go to **Group settings**.
3. Check **Managed group**.
4. Under **Group managers**, check every tenant owner or tenant manager who should filter Observability for this group.
5. Click **Create group** or **Save changes**.
6. On **Resources**, share the agents and datasets this group should use. The same agent can be shared into more than one managed group.

## Why this matters

A managed group gives each assigned manager an Observability filter for the people in that group. More than one manager means coverage does not depend on a single person, and an agent can serve several managed groups without blocking inference when their budget pools differ.

## Details

### Who can be a group manager

The **Managed group** hint states: unlock an Observability filter for the selected group managers. Tenant owners and tenant managers are eligible, and you can assign more than one.

The **Group managers** list shows each eligible person’s name and tenant role. Select one or more people. Each assigned manager can filter Observability to this group. If you check **Managed group** and select nobody, save is refused until at least one manager is selected.

Additional managers are members of the group with group-manager access. The **Overview** tab counts them under **Group managers**.

### What members can see

Any tenant user who can open the group can review **Members** and **Resources**. Invite, remove, and share actions stay with people who can manage the group. A row you cannot change is view-only.

### Share one agent into several managed groups

Share the agent from each group’s **Resources** tab, or from the agent’s **Group** visibility picker. Inference is allowed when those groups use different budget pools.

- When the person running the agent belongs to exactly one of those budget pools, the call is charged to that group.
- Otherwise the call continues on that person’s own budget.

On [Observability](gen3/observability) **Billing**, **Top managers** is a person, or **No assigned manager** when the request was not charged to a group manager budget. See [Group Spend](gen3/observability/group-spend).

### Agent catalog Group filter

On **Agents**, the **Group** filter on **Favorite Agents** and the agent catalog lists agents shared into that group. An agent you have not shared into the group stays out of that filtered list.

## Related pages

- [Groups](gen3/groups)
- [Managing Membership and Sharing](gen3/groups/managing-membership)
- [Limited Models](gen3/groups/limited-models)
- [Sharing Agents](gen3/agents/sharing)
- [Group Spend](gen3/observability/group-spend)
