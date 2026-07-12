---
description: Ensures the correct order of actions while developing a new feature (or fixing a bug) in an established project.
---

Follow these steps in order. Do not skip steps or reorder them.

## 1. Understand the request

- Read any specification, issue, or description the user has provided.
- Read related files and documents added to the context.
- If anything is ambiguous — requirements, scope, expected behavior, edge cases — ask the user before proceeding. Do not guess.

## 2. Explore the codebase

- Locate the relevant modules, files, and patterns that the new feature or fix will touch.
- Understand existing conventions: naming, structure, error handling, logging.
- Identify any existing tests that cover the area you're about to change.

## 3. Plan

- Write a short implementation plan (in your response, not a file).
- Identify which files will change and why.
- Flag any risks or trade-offs.
- Get explicit user sign-off before writing any code.

## 4. Update or write tests first

- If tests already exist for the affected code, update them to reflect the new expected behavior.
- If no tests exist, write them now.
- Tests should fail at this point — that confirms they actually verify the new behavior.

## 5. Implement

- Write the code to make the tests pass.
- Follow existing conventions; do not introduce new patterns unless necessary.
- Keep changes focused on the task — no incidental refactoring.

## 6. Verify

- Run the tests and confirm they pass.
- Check that no existing tests were broken.
- If the change affects UI, start the dev server and verify visually.

## 7. Report back

- Summarize what changed and why in one or two sentences.
- Note anything left out of scope that the user should be aware of.


## TODO
- You are a experienced senior analyst (check translation), help me flesh out a specc draft. use yaml with the structure of...
- Create a separate yaml file for holding the requirements.
- used requirement ids-
