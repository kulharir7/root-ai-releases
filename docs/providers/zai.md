---
summary: "Use Z.AI (GLM models) with Root"
read_when:
  - You want Z.AI / GLM models in Root
  - You need a simple ZAI_API_KEY setup
title: "Z.AI"
---

# Z.AI

Z.AI is the API platform for **GLM** models. It provides REST APIs for GLM and uses API keys
for authentication. Create your API key in the Z.AI console. Korvus uses the `zai` provider
with a Z.AI API key.

## CLI setup

```bash
Korvus onboard --auth-choice zai-api-key
# or non-interactive
Korvus onboard --zai-api-key "$ZAI_API_KEY"
```

## Config snippet

```json5
{
  env: { ZAI_API_KEY: "sk-..." },
  agents: { defaults: { model: { primary: "zai/glm-5" } } },
}
```

## Notes

- GLM models are available as `zai/<model>` (example: `zai/glm-5`).
- See [/providers/glm](/providers/glm) for the model family overview.
- Z.AI uses Bearer auth with your API key.
