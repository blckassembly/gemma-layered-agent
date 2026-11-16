# Adapters

Slots declared in `agent.yaml`:

- `main_lora/` — primary task adapter (post-trained Gemma 4 weights land here)
- `tool_lora/` — tool-use adapter

Both are placeholders in v0.1. The workflow runs on prompts + config
alone; adapters are the post-training step, not a prerequisite for
testing the architecture on the practice task set.
