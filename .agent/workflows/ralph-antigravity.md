---
description: Start the autonomous Ralph development loop with Architecture 7.0 Resilience
---

# Ralph-Antigravity Workflow (Resilient Edition)

This workflow executes an iterative development loop with task-specific branching and failure recovery.

## Workflow Logic (Artifact-Driven Loop)

1. **Phase 1: Sync & Select**
   - Run `python src/github_sync.py` to sync PRDs.
   - Run `python src/ralph_controller.py next` to pick the next task.
   - **Architecture 7.0**: This command automatically creates a unique branch (e.g., `ralph/issue-123`) and tracks the attempt count (max 5).

2. **Phase 2: Context Discovery**
   - Run `python src/ralph_controller.py discover "[Task Title]"` to identify relevant files.
   - Gathers "Context Anchors" to ensure domain knowledge is preserved.

3. **Phase 3: Planning (Required)**
   - Analyze requirements and create `implementation_plan.md`.
   - **Important**: Plan must explicitly mention any documentation files that need updating.

4. **Phase 4: Implementation**
   - Execute code changes on the task-specific branch.
   - Update `task.md` to reflect progress.

5. **Phase 5: Verification & Walkthrough**
   - Run tests and linting.
   - **Multimodal Check**: Use vision for UI tasks.
   - Create `walkthrough.md`.
   - **Failure Handling**: If verification fails, run `python src/ralph_controller.py fail [task_id]` and retry Phase 3.

6. **Phase 6: Documentation Maintenance (New in 7.0)**
   - **Mandatory**: Review `README.md`, `ARCH.md`, or files in `docs/`.
   - Update them to reflect the new implementation details.

7. **Phase 7: Automated Audit & Closure**
   - Commit all changes to the task branch.
   - Run `python src/ralph_controller.py finish`.
   - **Architecture 7.0**: Automatically pushes the branch to remote and closes the GitHub issue.

8. **Iterate**
   - Return to Phase 1.
