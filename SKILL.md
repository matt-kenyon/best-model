---
name: best-model
description: Assess a task or prompt and recommend the best available Codex model and reasoning effort for it. Use when the user invokes `$best-model` or `/best-model`, appends `best-model` to a task, asks which model should handle a task, or wants a quality, speed, and cost tradeoff before beginning work.
---

# Best Model

Assess the attached task or prompt. Recommend a model; do not perform the underlying task unless the user explicitly asks to continue afterward.

## Process

1. Identify the task's dominant demands: complexity, ambiguity, coding depth, research, tool use, visual judgment, context size, stakes, and expected duration.
2. Infer the user's priority from the prompt. Default to the best quality-to-time tradeoff when quality, speed, and cost are not specified.
3. Consider only models actually available in the user's current Codex environment. Do not confuse API availability with availability in the Codex model picker.
4. When model names, capabilities, or availability may be stale or unclear, use the OpenAI Docs skill or current official OpenAI documentation before recommending. Prefer role-based reasoning over a hard-coded model catalog.
5. Select the least expensive and fastest model likely to complete the task reliably. Escalate to the frontier model when errors would be costly, the task requires deep cross-file or multi-step reasoning, requirements are ambiguous, or the output needs unusually strong judgment.
6. Recommend a reasoning effort supported by the selected model:
   - `low` for straightforward, well-scoped work and quick transformations.
   - `medium` as the balanced default.
   - `high` for difficult implementation, research synthesis, debugging, or consequential review.
   - `xhigh` for unusually complex, ambiguous, or high-stakes work where extra latency is justified.
   - `max` only for the hardest quality-first tasks when the likely gain justifies substantial latency and cost.
7. Mention a cheaper or faster alternative only when it represents a meaningful tradeoff.

## Response format

Keep the recommendation brief:

**Best model:** `<model>` with `<reasoning effort>`

**Why:** One or two sentences tied to the actual task.

**Alternative:** `<model>` with `<reasoning effort>` — one short tradeoff sentence. Omit when it adds no value.

If the user's requested task lacks enough information to distinguish between materially different choices, ask one concise question instead of guessing.
