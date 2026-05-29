# Sharing Agents

## Start Here

1. Open the agent in **Agent Configuration**.
2. Review visibility: private, group, or tenant-wide as your role allows.
3. Share into a [Group](gen3/groups) when collaboration should inherit membership boundaries.
4. Confirm collaborators see the agent in their catalog before announcing availability.

## Why this matters

Sharing controls prevent accidental tenant-wide exposure of experimental agents and align access with group membership policy.

## Details

Agent sharing in Gen 3 only works well when the agent's supporting context is shareable too. Before you share an agent, confirm that its datasets, assumptions, and visibility all match the audience you intend.

## Sharing decisions to make first

Review these questions before changing visibility:

1. Should the agent stay private to its owner?
2. Should it be shared only with a specific [group](gen3/groups)?
3. Does it depend on datasets that other users cannot access?
4. Do the instructions include assumptions that only make sense for one team or role?

## Group sharing vs broader visibility

### Use group sharing when

- the agent belongs to a specific operational unit
- the supporting datasets are already group-scoped
- the workflow should stay inside a managed collaboration boundary

### Use broader visibility when

- the agent is safe and useful for a wider tenant audience
- the underlying datasets are also visible to that same audience

## The dependency rule

An agent shared to other users is only as useful as the resources behind it. If the agent relies on a private dataset, other users may see the agent but still fail to get grounded answers. Review dataset posture on [Datasets](gen3/datasets) before troubleshooting the agent itself.

## Recommended sharing workflow

1. Finalize the agent behavior.
2. Confirm the attached datasets are visible to the intended audience.
3. Share the agent to the correct scope.
4. Validate the result with a real user or a test account that has the target visibility.

## Best practices

- Share to the narrowest scope that still fits the work.
- Use [Groups](gen3/groups) for team-owned or managed-workflow agents.
- Avoid sharing half-configured agents that still depend on private draft datasets.
- Re-test after every visibility change.

## Related pages

- [Groups](gen3/groups)
- [Managing Membership and Sharing](gen3/groups/managing-membership)
- [Datasets](gen3/datasets)
