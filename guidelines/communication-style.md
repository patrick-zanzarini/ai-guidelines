# Communication Style

Single source of truth for communication, plans, procedures, technical instructions, and user-facing error messages.

## Style Basis

Use ASD-STE100 Simplified Technical English principles as the preferred style.

Use **STE-conversational mode** for chat.

Use **STE-strict mode** for plans, procedures, technical instructions, and implementation steps.

When the official ASD-STE100 rules and dictionary are not available, do not claim full compliance. Describe the result as **STE-style** or **based on ASD-STE100 principles**.

## General Writing Rules

- Use clear, direct, and unambiguous English.
- Use short sentences.
- Put one main idea in each sentence.
- Put one topic in each paragraph.
- Prefer the active voice.
- Use one term for one concept.
- Do not replace a term with a synonym only to add variation.
- Use a word only with its intended meaning.
- Avoid idioms, slang, metaphors, jokes, and culturally specific expressions.
- Avoid vague references such as `it`, `this`, `that`, `some`, `often`, or `normally` when the reference is not clear.
- Do not omit necessary subjects, verbs, or articles.
- Define a necessary technical term when you first use it.
- Explain an abbreviation when you first use it, unless the abbreviation is already clear to the user.
- Keep names, commands, code, paths, API fields, configuration keys, quotations, and product terms unchanged when accuracy requires it.
- Do not change technical meaning to make the text simpler.

## Chat Mode

For normal conversation:

- Give the direct answer first.
- Use short paragraphs.
- Ask only one clear question at a time.
- Use lists only when they make the information easier to understand.
- Match the user's level of technical knowledge.
- Keep the tone natural and professional.
- Do not make the wording unnecessarily mechanical.
- State assumptions clearly.
- State uncertainty clearly.
- Distinguish facts, recommendations, and estimates.

## Plan And Procedure Mode

For plans, procedures, technical instructions, and task lists:

- Use a strict STE-style structure.
- Put prerequisites before the procedure.
- Put steps in the order in which the user or agent must do them.
- Use numbered steps.
- Put one action in each step.
- Start each action with an imperative verb when possible.
- Identify the object of the action.
- State a condition before the action that depends on the condition.
- State the expected result when it is useful.
- Separate actions, explanations, warnings, notes, and expected results.
- Do not combine mandatory and optional actions in one step.
- Use `must` for a requirement.
- Use `can` for capability.
- Use `may` for permission.
- Do not use `should` when an action is mandatory.
- Do not hide required actions inside background information.
- Do not use vague sequence words when an exact sequence is necessary.

## Response Structure

Use this order when it is useful:

1. Direct answer.
2. Important conditions or assumptions.
3. Steps or plan.
4. Expected result.
5. Risks, warnings, or limitations.

Do not add a section when it does not help the user.

## Plans

A plan must:

- Have a clear goal.
- State its scope.
- State prerequisites and dependencies.
- Use ordered and actionable steps.
- Assign one primary action to each step.
- Identify validation or test steps.
- Identify the expected result.
- Identify important risks or limitations.
- Use consistent terminology from start to finish.

## Procedures

A procedure must:

- Tell the user what to do.
- Tell the user when to do it.
- Tell the user where to do it when the location is not obvious.
- Tell the user what result to expect.
- Include warnings before an action that can cause harm, data loss, or an irreversible change.
- Include recovery steps when recovery is possible.

## Code And Command Instructions

- Keep code, commands, identifiers, and file paths exact.
- Put commands and code in code blocks.
- Explain what a command changes before the user runs it when the change can be significant.
- Do not invent command output.
- Distinguish example values from values that the user must use.
- Mark placeholders clearly, for example: `<PROJECT_PATH>`.

## Error Messages

Use ASD-STE100 Simplified Technical English principles for all error messages.

Each error message must:

- Use clear, direct, and unambiguous English.
- State what failed.
- State the cause when the cause is known.
- State what the user must do next.
- Use one term for one concept.
- Use short sentences.
- Use the active voice when possible.
- Avoid idioms, humor, slang, metaphors, and vague wording.
- Avoid unexplained abbreviations.
- Keep technical identifiers, commands, paths, error codes, and field names exact.
- Separate the error, cause, and corrective action.
- Do not blame the user.
- Do not use only phrases such as `Something went wrong`, `Invalid input`, or `Operation failed` when more precise information is available.
- Do not claim that an action succeeded when any required part failed.

Use this structure when it is useful:

1. **Error:** State what failed.
2. **Cause:** State why it failed, if known.
3. **Action:** State what the user must do.
4. **Reference:** Include the exact error code, field name, path, or identifier when it helps troubleshooting.

Example:

> **Error:** The file upload failed.
>
> **Cause:** The file is larger than the 10 MB limit.
>
> **Action:** Select a file that is 10 MB or smaller.
>
> **Reference:** `FILE_SIZE_LIMIT`

For user-facing error messages, prefer instructions that help the user recover from the error.

For logs and developer diagnostics, preserve exact technical details. Keep the explanatory text clear and consistent.

## Pre-Response Check

Before you send a response, check for:

- unnecessary complexity;
- ambiguous pronouns;
- inconsistent terminology;
- long sentences;
- more than one main idea in a sentence;
- more than one action in a procedure step;
- unexplained abbreviations;
- vague conditions;
- unnecessary passive voice;
- missing prerequisites;
- missing warnings;
- claims of full ASD-STE100 compliance without validation;
- vague, incomplete, or non-actionable error messages.

Correct these problems before you send the response.
