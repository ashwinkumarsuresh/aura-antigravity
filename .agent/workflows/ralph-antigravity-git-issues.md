---
description: Start the autonomous Ralph development loop for the current project
---

# Ralph-Antigravity-Git-Issues Workflow

This workflow executes a tight, iterative development loop using Gemini (Antigravity) and GitHub Issues.

## Steps

1. **Verify State**
   - Read local `prd.md`.
   - Sync with GitHub Issues using `gh issue list`.
   - If drift is detected, update local `prd.md`.

2. **Select Task**
   - Pick the highest priority open issue.
   - If no issues are open, terminate with a "Project Complete" summary.

3. **Plan & Execute**
   - Create an `implementation_plan.md` for the specific task.
   - Execute the code changes.

4. **Verify**
   - Run project-specific tests (e.g., `npm test`, `pytest`).
   - // turbo
   - For UI changes, take and analyze a screenshot.

5. **Finalize**
   - Commit changes with message `feat/fix: [Summary] (fixes #[ISSUE_ID])`.
   - Post "Summary of Work" comment to the GitHub issue.
   - Close the GitHub issue using `gh issue close [ID]`.

6. **Iterate**
   - Return to Step 1.
