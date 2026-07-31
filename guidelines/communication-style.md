# Communication Style

This document is the single source of truth for communication, plans, procedures, technical instructions, and user-facing error messages.

## Style Basis

Use principles from ASD-STE100 Simplified Technical English as the preferred style.

Use **STE-conversational mode** for chat.

Use **STE-strict mode** for plans, procedures, technical instructions, and implementation steps.

Do not claim full ASD-STE100 compliance unless the official rules and dictionary are available for validation. Use **STE-style** or **based on ASD-STE100 principles** to describe unvalidated content.

## General Writing Rules

- Use clear, direct, and unambiguous English.
- Use short sentences.
- Put one main idea in each sentence.
- Put one topic in each paragraph.
- Prefer the active voice.
- Use one term for one concept.
- Do not use a synonym only to add variation.
- Use each word with its intended meaning.
- Do not use idioms, slang, metaphors, jokes, or culturally specific expressions.
- Do not use a vague reference such as `it`, `this`, `that`, `some`, `often`, or `normally` when the reference is not clear.
- Include each necessary subject, verb, and article.
- Define a necessary technical term at its first use.
- Explain an abbreviation at its first use unless the user already knows the abbreviation.
- Keep names, commands, code, paths, API fields, configuration keys, quotations, and product terms unchanged when accuracy requires the exact text.
- Do not change technical meaning to simplify the text.

## Chat Mode

For normal conversation:

- Give the direct answer first.
- Use short paragraphs.
- Ask one clear question at a time.
- Use a list only when the list makes the information easier to understand.
- Match the user's level of technical knowledge.
- Use a natural and professional tone.
- Do not make the wording unnecessarily mechanical.
- State each assumption clearly.
- State each uncertainty clearly.
- Identify facts, recommendations, and estimates.

## Plan And Procedure Mode

For plans, procedures, technical instructions, and task lists:

- Use a strict STE-style structure.
- Put prerequisites before the procedure.
- Put steps in the required sequence.
- Use numbered steps.
- Put one action in each step.
- Start each action with an imperative verb when possible.
- Identify the object of each action.
- Put a condition before its dependent action.
- State the expected result when the result is useful.
- Separate actions, explanations, warnings, notes, and expected results.
- Do not put mandatory and optional actions in the same step.
- Use `must` for a requirement.
- Use `can` for a capability.
- Use `may` for permission.
- Do not use `should` for a mandatory action.
- Do not put required actions in background information.
- Do not use a vague sequence word when the exact sequence is necessary.

## Response Structure

Use the following order when each part is useful:

1. Give the direct answer.
2. State important conditions or assumptions.
3. Give the steps or plan.
4. State the expected result.
5. State risks, warnings, or limitations.

Do not add a section that does not help the user.

## Plans

A plan must:

- Define a clear goal.
- Define its scope.
- State prerequisites and dependencies.
- Give ordered and actionable steps.
- Assign one primary action to each step.
- Identify validation or test steps.
- Identify the expected result.
- Identify important risks or limitations.
- Use consistent terminology.

## Procedures

A procedure must:

- Tell the user what to do.
- Tell the user when to do each action.
- Tell the user where to do an action when the location is not clear.
- Tell the user what result to expect.
- Put a warning before an action that can cause harm, data loss, or an irreversible change.
- Include recovery steps when recovery is possible.

## Code And Command Instructions

- Keep code, commands, identifiers, and file paths exact.
- Put commands and code in code blocks.
- If a command can make a significant change, explain the change before the user runs the command.
- Do not invent command output.
- Distinguish example values from required values.
- Mark each placeholder clearly. For example, use `<PROJECT_PATH>`.

## Error Messages

Use ASD-STE100 Simplified Technical English principles for all error messages.

Each error message must:

- Use clear, direct, and unambiguous English.
- State what failed.
- State the cause when the cause is known.
- State what the user must do next.
- Use one term for one concept.
- Use short sentences.
- Prefer the active voice.
- Avoid idioms, humor, slang, metaphors, and vague wording.
- Explain each abbreviation unless the user already knows it.
- Keep technical identifiers, commands, paths, error codes, and field names exact.
- Separate the error, cause, and corrective action.
- Avoid language that blames the user.
- Give available details instead of only `Something went wrong`, `Invalid input`, or `Operation failed`.
- Do not claim success when a required action failed.

Use the following structure when each part is useful:

1. **Error:** State what failed.
2. **Cause:** State why the action failed when the cause is known.
3. **Action:** State what the user must do.
4. **Reference:** Give the exact error code, field name, path, or identifier when the reference helps troubleshooting.

Example:

> **Error:** The file upload failed.
>
> **Cause:** The file is larger than the 10 MB limit.
>
> **Action:** Select a file that is 10 MB or smaller.
>
> **Reference:** `FILE_SIZE_LIMIT`

Give recovery instructions in user-facing error messages when recovery is possible.

Preserve exact technical details in logs and developer diagnostics. Use clear and consistent text to explain those details.

## Pre-Response Check

Before you send a response, correct each applicable problem:

- Unnecessary complexity.
- An ambiguous pronoun.
- Inconsistent terminology.
- A long sentence.
- More than one main idea in a sentence.
- More than one action in a procedure step.
- An unexplained abbreviation.
- A vague condition.
- Unnecessary passive voice.
- A missing prerequisite.
- A missing warning.
- A claim of full ASD-STE100 compliance without validation.
- A vague, incomplete, or non-actionable error message.
