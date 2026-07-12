---
description: Ensures the correct order of actions while fixing a bug in an established project.
---

Follow these steps in order. Do not skip steps or reorder them.

## 1. Reproduce the bug

- Read the bug report, issue, or description the user has provided.
- Reproduce the failure yourself and confirm you can trigger it reliably before doing anything else.
- Capture the exact steps, inputs, and observed vs. expected behavior.
- If you cannot reproduce it, ask the user for the missing details — do not guess.

## 2. Find the root cause

- Trace the failure back to the code that produces it. Don't stop at the symptom.
- Understand existing conventions: naming, structure, error handling, logging.
- Identify any existing tests that cover — or should have caught — the area.
- Confirm the root cause explains the full behavior you observed in step 1.

## 3. Plan the fix

- Prefer the smallest fix that addresses the root cause, not the symptom; call out any place the plan trades a proper fix for a workaround.
- Write a short plan (in your response, not a file): what changes, why, and the files affected.
- Flag any risks, side effects, or related code paths the fix might touch.
- Get explicit user sign-off before writing any code.

## 4. Write a failing test that captures the bug

- Add a test that reproduces the bug and fails for the reason you identified in step 2.
- Run it and confirm it fails — that proves the test actually catches this bug.
- If the bug isn't meaningfully unit-testable, say so and state how you'll verify the fix instead.

## 5. Fix

- Write the minimal code to make the failing test pass.
- Follow existing conventions; do not introduce new patterns unless necessary.
- Keep changes focused on the fix — no incidental refactoring.
- If the fix reveals the root cause was wrong, stop and re-confirm before proceeding.

## 6. Verify

- Run the new test and confirm it now passes.
- Re-run the original reproduction from step 1 and confirm the bug is gone.
- Run the full test suite and confirm no existing tests were broken.
- Run lint, typecheck, and build if the project has them.

## 7. Report back

- Summarize the root cause and the fix in one or two sentences.
- Note anything left out of scope that the user should be aware of.
- Note what you're least confident about right now.
- Note what's the biggest thing we might be missing about the situation right now.
