# Agent Capabilities

## Start Here

1. Open **Agents** → **Agent Configuration** and open the agent.
2. In **Agent Settings**, open the modality tab you want to change.
3. Set the access control to **Disabled** to turn that capability off for this agent, or leave it **Enabled**.
4. Save the agent.
5. Open **GT Chat** with that agent and confirm the matching action is gone.

## Why this matters

One agent can stay text-only while another on the same deployment still transcribes audio, reads replies aloud, analyzes images, or generates images. Existing agents stay **Enabled** until you change them, so a save that does not touch these controls keeps current chat behavior.

## Details

These switches are per agent. They do not remove the model from the deployment. To keep a model out of a capability for every agent, a Control Panel operator unchecks that modality on the model. See [Model Capabilities](gen3-admin/models/capabilities).

A tab appears when the deployment has that class of model enabled. If a tab is missing, the deployment does not currently offer that capability.

| Tab | Access control | What **Disabled** does |
| --- | --- | --- |
| **Vision Settings** | **Vision access** | This agent is not offered image analysis. |
| **STT / TTS Settings** | **Speech-to-text access** | This agent cannot transcribe microphone or uploaded audio. The deployment can still have speech-to-text turned on. |
| **STT / TTS Settings** | **Text-to-speech access** | This agent cannot read replies aloud or use hands-free spoken replies. |
| **Image Generation Settings** | **Image generation access** | This agent cannot create images in chat or through the GT API. |

Choosing **Disabled** greys out that tab’s model and option fields. Choosing **Enabled** restores them. Chat and GT API routes for a disabled capability are rejected for that agent.

**Chat Model Settings** and **Web Search Settings** are separate. Web search still follows **Web search access** on that tab. See [Building Agents](gen3/agents/building).

### Suggested checks

1. With vision **Disabled**, confirm image analysis is not offered in **GT Chat**.
2. With speech-to-text **Disabled**, confirm microphone and audio upload transcription are unavailable.
3. With text-to-speech **Disabled**, confirm Read Aloud and hands-free spoken replies are unavailable.
4. With image generation **Disabled**, confirm Create Image is unavailable in chat and that a GT API image call for that agent is rejected.
5. Open a second agent that you left **Enabled** and confirm its actions are unchanged.

If the agent uses a [limited model](gen3/groups/limited-models), review every modality tab before you share it. Each limited model on the agent must be available to the groups you share with.

## Related pages

- [Building Agents](gen3/agents/building)
- [GT Chat](gen3/chat)
- [Model Capabilities](gen3-admin/models/capabilities)
- [GT API Addresses](gen3/gt-api/addresses)
