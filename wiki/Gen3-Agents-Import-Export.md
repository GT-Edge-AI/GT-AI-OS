# Importing and Exporting Agents

## Start Here

1. Open **Agents** → **Agent Configuration**.
2. Click **Export Agent**, choose the agents, and export. One agent downloads as CSV. Several agents download as a ZIP of those CSVs.
3. On the target tenant, click **Import Agent**.
4. Drop the CSV or ZIP. CSV files can be up to 1 MiB. ZIP files can be up to 10 MiB.
5. After import, open any agent that shows **No model selected** and choose a Text Chat LLM on **Chat Model Settings**.

## Why this matters

Exports travel by the provider model name, such as `openai/gpt-oss-120b`, in the CSV `model` column. The target tenant matches that name in its own catalog. A catalog row id from the source tenant is not required, so the same file can land in another environment.

## Details

**Import Agent** and **Export Agent** move saved agent definitions. They are separate from **Agent Templates**, which loads starters from the instructions catalog. See [Building Agents](gen3/agents/building).

### What the `model` column contains

Current exports write the provider model name. Import looks up that name in the target catalog.

When the name is missing from the target catalog, import still creates the agent and leaves the model blank. **Favorite Agents**, the agent catalog, and the agent editor show **No model selected** until you choose a Text Chat LLM.

Older CSV files that still contain a source catalog row id import the same way: the agent is added, and the model stays blank when that id is not in the target catalog.

### Import behavior

The import shelf accepts `.csv` and `.zip` files. Arrays use `|` inside a single CSV cell. Dataset columns accept ids or names. Duplicate agent names are renamed automatically. Team columns resolve against groups in this tenant by the imported team name.

Attached datasets, visibility, and modality fields come from the file. A model name that does not exist here is the field you fix after import. Walk **Vision Settings**, **STT / TTS Settings**, **Image Generation Settings**, and **Web Search Settings** before you share the agent. See [Agent Capabilities](gen3/agents/capabilities).

### Move an agent to another tenant

1. Export from the source **Agent Configuration** workspace.
2. Confirm the target tenant’s [Model Catalog](gen3/model-catalog) includes the provider model name you need, or plan to pick a replacement after import.
3. Import on the target tenant.
4. Open each imported agent, set **Chat Model Settings** when the card says **No model selected**, and confirm datasets resolved.
5. Set **Visibility** again if the target groups use different names. See [Sharing Agents](gen3/agents/sharing).

## Related pages

- [Agents](gen3/agents)
- [Building Agents](gen3/agents/building)
- [Sharing Agents](gen3/agents/sharing)
- [Model Catalog](gen3/model-catalog)
