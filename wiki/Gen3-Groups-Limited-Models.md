# Limited Models

## Start Here

1. Sign in as a **tenant owner**. Tenant managers and tenant users do not see this control.
2. Open **Groups**, then open the group that should keep the model.
3. Open **Group settings**.
4. Under **Limited models**, search if needed and check each model that should stay inside selected groups.
5. Click **Save changes**.
6. Open the agent that uses that model and set **Visibility** to **Group**, then share it only with groups that can use every limited model on the agent.

## Why this matters

A limited model stays off the catalog and agent pickers for people who are not in a group that has it. That keeps a specialty or licensed model inside the teams that are supposed to use it, and it stops an agent that depends on that model from being published to the whole organization.

## Details

**Limited models** is on the group workspace **Group settings** tab. It is not on the **New group** form. Create the group first, then open it and limit models there.

The helper under **Limited models** states the rule: models checked here are hidden from people who are not in a group that has the model. An agent that uses one of these models cannot be shared with the organization. It can only be shared with groups that also have access to that model.

Leave a model unchecked when everyone in the tenant should still see it.

### Who can see a limited model

A person sees a limited model when they belong to at least one group where that model is checked. The same model can be checked on more than one group. People outside all of those groups do not see it in the model catalog or in agent model pickers.

### Sharing an agent that uses a limited model

On **Agent Configuration**, **Visibility** offers **Individual** and **Group**. **Organization** is unavailable while any model on the agent is limited.

The group picker lists only groups that can use every limited model on that agent. If the agent uses two limited models that are not both available to the same group, the helper reads: **The models on this agent are limited to different groups, so it cannot be shared. Keep it individual, or change one of the models.**

When a valid group exists, the helper reads: **This agent uses a group-limited model. It cannot be shared with the organization, and it can only be shared with groups that have access to every limited model on the agent.**

Chat, vision, speech, image, and web-search models on the agent all count. Review each modality tab before you share. See [Agent Capabilities](gen3/agents/capabilities) and [Sharing Agents](gen3/agents/sharing).

### After you change the checkboxes

1. Confirm a member of the group can still select the model.
2. Confirm an account outside those groups no longer sees it.
3. Re-open any agent that used the model and confirm **Visibility** still matches the groups that can run it.

## Related pages

- [Groups](gen3/groups)
- [Group Managers](gen3/groups/managers)
- [Sharing Agents](gen3/agents/sharing)
- [Model Catalog](gen3/model-catalog)
