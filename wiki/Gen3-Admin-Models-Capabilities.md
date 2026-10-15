# Model Capabilities

## Start Here

1. Open **Models** → **Configured Models** and edit the model.
2. Find the **Capabilities** section.
3. Uncheck **Image in**, **Image out**, **Speech to text**, or **Text to speech** to keep this model out of that capability.
4. Save the model.
5. In the tenant app, confirm the model no longer appears for that capability on an agent’s matching settings tab.

## Why this matters

A model can stay available for text chat while vision, image generation, or speech is turned off for that model alone. Agents can also turn the same capabilities off for one agent without changing the model. See [Agent Capabilities](gen3/agents/capabilities).

## Details

The **Capabilities** note on the model form states: these switches are per model. Uncheck a modality to stop this model from being offered for that capability. **Image out** turns off image generation, **Image in** turns off vision, and the speech checkboxes turn off speech-to-text or text-to-speech.

| Checkbox | Effect when unchecked |
| --- | --- |
| **Image in** | Vision is off for this model. Agents and image-analysis routes will not use it. |
| **Image out** | Image generation is off for this model. Create Image and image API routes will not use it. |
| **Speech to text** | Speech-to-text is off for this model. |
| **Text to speech** | Text-to-speech is off for this model. |

**Text in**, **Text out**, **Audio in**, **Audio out**, **Streaming**, **Tool use**, **Web search**, and **Embeddings** remain on the same form. Leave **Tool use** checked when this model is a Text Chat LLM for agents that call datasets, web search, image tools, or Contextual Memory.

Unchecking a modality here removes the model from that capability across agents. Disabling the same capability on one agent leaves the model available to other agents.

## Related pages

- [Models](gen3-admin/models)
- [Agent Capabilities](gen3/agents/capabilities)
- [Model Catalog](gen3/model-catalog)
