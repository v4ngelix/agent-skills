---
description: Ensures the correct order of actions while developing a new feature in an established project.
---

Follow these steps in order. Do not skip steps or reorder them.

## 1. Understand the request

- Read any specification, issue, or description the user has provided.
- Read related files and documents added to the context.
- If anything is ambiguous — requirements, scope, expected behavior, edge cases — ask the user before proceeding. Do not guess.

## 2. Explore the codebase

- Locate the relevant modules, files, and patterns that the new feature will touch.
- Understand existing conventions: naming, structure, error handling, logging.
- Identify any existing tests that cover the area you're about to change.

## 3. Plan

- Prefer the simplest design that fits existing conventions; call out any place the plan trades simplicity for flexibility.
- Write a short implementation plan (in your response, not a file).
- Identify which files will change and why.
- Flag any risks or trade-offs.
- Get explicit user sign-off before writing any code.

## 4. Update or write tests first

- If tests already exist for the affected code, update them to reflect the new expected behavior.
- If no tests exist, write them now.
- Tests should fail at this point — that confirms they actually verify the new behavior.
- If the change isn't meaningfully unit-testable (config, wiring, some UI), say so and state how you'll verify it instead.

## 5. Implement

- Write the code to make the tests pass.
- Follow existing conventions; do not introduce new patterns unless necessary.
- Keep changes focused on the task — no incidental refactoring.
- If implementation reveals the plan was wrong, stop and re-confirm before proceeding.

## 6. Verify

- Run the tests and confirm they pass.
- Check that no existing tests were broken.
- Run lint, typecheck, and build if the project has them.
- If the change affects UI, start the dev server and verify visually.

## 7. Report back

- Summarize what changed and why in one or two sentences.
- Note anything left out of scope that the user should be aware of.
- Note what you're least confident about right now.
- Note what's the biggest thing we might be missing about the situation right now.
