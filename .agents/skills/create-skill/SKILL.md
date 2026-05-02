---
name: create-skill
version: 0.1.0
description: |
  Turn a conversational workflow or recurring development methodology into a
  reusable `SKILL.md` that other agents or contributors can invoke. This
  skill codifies the step-by-step process, decision points, quality checks,
  and example prompts needed to reproduce the workflow consistently.
---

When to use
-----------
- Use when a conversation has produced a repeatable multi-step workflow.
- Use to capture project-specific workflows that should be re-run or
  recommended by an assistant (e.g., TDD cycles, handoff procedures, agent
  customization steps).

Purpose
-------
- Explain the stepwise process to convert a conversation into a SKILL.
- Provide a checklist and decision points for ambiguous choices.
- Produce a draft `SKILL.md` saved in the repository and a short set of
  follow-up questions to resolve ambiguity.

Step-by-step process
--------------------
1. Extract the workflow: identify discrete steps described in the
   conversation and group them into an ordered list.
2. Identify decision points: where the flow can branch or requires
   user choices (e.g., test-first vs implement-first, repo vs personal).
3. Define completion criteria: what constitutes 'done' for each step
   (tests passing, PR opened, files updated).
4. Draft SKILL.md: write clear usage guidance, inputs, outputs, and
   explicit prompts the assistant should use.
5. Save draft to the workspace under `.agents/skills/<skill-name>/SKILL.md`.
6. Highlight ambiguous items and ask targeted clarifying questions.
7. Iterate: update the SKILL.md until acceptance criteria are met.

Decision points and branching logic
-----------------------------------
- Scope: workspace-scoped (committed to repo) vs personal (local only).
- Test requirement: require a failing test first (TDD) or optional tests.
- Automation level: fully automated edits vs guided edits requiring user
  confirmation.

Quality criteria / completion checks
-----------------------------------
- Steps are actionable and numbered.
- Decision points are explicit with recommended defaults.
- Example prompts are provided for common invocations.
- Location and filenames to edit are specified as workspace-relative links.
- Suggest tests or test templates when the workflow modifies behavior.

Ambiguities to ask about (typical)
----------------------------------
- Should the skill be saved in the repository (`.agents/skills/`) or only
  provided to the user as a clipboard draft?
- Should the skill mandate TDD (create failing test first)?
- Preferred file naming and example prompt style (concise vs verbose)?

Iterate
-------
1. Draft and save the SKILL.md.
2. Return a short list of ambiguous items (above) to the user.
3. After user clarifies, update the SKILL.md and mark it final.

Example prompts to try
----------------------
- "Create a SKILL.md from the last conversation, saving it to
  `.agents/skills/create-skill/SKILL.md`."
- "Extract the TDD workflow we discussed and make it a reusable skill
  that enforces writing a failing test first."

What this SKILL produces
------------------------
- A repository file at `.agents/skills/<skill-name>/SKILL.md` containing:
  - Purpose and when to use the skill
  - A step-by-step process
  - Decision points and quality checks
  - Example prompts and next steps

Related customizations to consider
---------------------------------
- Add `.instructions.md` showcasing example system prompts for the skill.
- Add a test template under `test/templates/` for workflows that require
  TDD.
- Add CI checks that ensure newly added skills meet a minimal checklist.

Next steps I recommend
----------------------
1. Confirm whether this skill should be workspace-scoped or personal.
2. Tell me whether TDD should be enforced by default.
3. If you confirm, I'll finalize this SKILL.md and add a short test
   template or example invocation in the repo.
