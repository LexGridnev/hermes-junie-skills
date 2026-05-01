---
name: workflow-distiller
description: Distill successful multi-step workflows into reusable Junie CLI skills. Use when a complex task (5+ turns, error recovery, or novel procedure) is completed to save procedural knowledge for future use.
---

# Workflow Distiller

You are an expert at procedural distillation. Your goal is to capture the "essence" of a successful workflow so that future instances of Junie CLI can replicate it without repeating your trial-and-error.

## Distillation Procedure

When you recognize a successful complex workflow, follow these steps:

### 1. Analyze the Trajectory
Review the current conversation history. Identify:
- **The Core Objective:** What was the user trying to achieve?
- **The Winning Sequence:** What specific tools and commands actually worked?
- **The Pitfalls:** What failed, and how did you overcome it? (e.g., "Don't use `grep` without `-E` for this pattern").
- **Dependencies:** What environment variables, tools, or files were required?

### 2. Draft the Skill
Create a generalized version of the workflow.
- **Name:** Follow the `skill-creator` naming rules (lowercase, hyphenated, verb-led).
- **Description:** Clear, single-line trigger description.
- **Body:** Use imperative instructions. Focus on the *how-to*. Use progressive disclosure (keep SKILL.md lean, link to references).

### 3. Save as a Skill
Use the `skill-creator` tools to build the package.

1. **Initialize:**
   ```bash
   node /data/data/com.termux/files/usr/lib/node_modules/@google/gemini-cli/bundle/builtin/skill-creator/scripts/init_skill.cjs <new-skill-name> --path ./skills
   ```
2. **Populate:** Write the `SKILL.md` and any necessary scripts/references into the new directory.
3. **Package:**
   ```bash
   node /data/data/com.termux/files/usr/lib/node_modules/@google/gemini-cli/bundle/builtin/skill-creator/scripts/package_skill.cjs ./skills/<new-skill-name>
   ```
4. **Offer Installation:** Present the `.skill` file to the user and offer to install it (`gemini skills install ...`).

## Writing Principles
- **Conciseness:** Don't explain *why* something works; just give the command.
- **Deterministic Scripts:** If a step involves complex text manipulation or repetitive logic, write a small script in the `scripts/` directory.
- **Verification:** Always include a "Verification" section in the new skill so the agent knows how to confirm success.

## Example Trigger Scenarios
- "I've successfully configured the custom Android build pipeline after several attempts. I should save this as `android-build-config` skill."
- "The user asked me to remember this specific data-cleaning workflow. I will distill it into `clean-user-data` skill."