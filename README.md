# Hermes-inspired Junie CLI Skills

This repository contains skills for the Junie CLI, adapted from the self-improving architecture of the [NousResearch/hermes-agent](https://github.com/nousresearch/hermes-agent).

## Included Skills

### 🧠 [Memory Manager](./memory-manager)
Safely manages persistent memory across Global, Workspace, and Private tiers.
- **Threat Scanning:** Manually scans all memory writes for prompt injections and exfiltration attempts.
- **Tiered Routing:** Maps facts to the correct Junie CLI memory tier.

### 📝 [Workflow Distiller](./workflow-distiller)
Distills successful multi-step workflows into reusable Junie CLI skills.
- **Trajectory Analysis:** Identifies the "winning sequence" of commands from conversation history.
- **Autonomous Drafting:** Generates new `SKILL.md` files from successful procedures.

## Installation

1. Clone this repository or download the `.skill` files.
2. Install a skill using the Junie CLI:
   ```bash
   gemini skills install path/to/skill-folder --scope user
   ```
3. Reload skills in your interactive session:
   ```bash
   /skills reload
   ```
