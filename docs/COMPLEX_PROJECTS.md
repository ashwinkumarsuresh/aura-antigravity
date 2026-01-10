# 🏗️ Managing Complex Projects with Ralph-Antigravity
## A Guide for Junior Developers

So you've graduated from a single-file script to a complex application with multiple modules? Welcome to the big leagues! Ralph-Antigravity is designed to scale with you. This guide explains how to use the **Architecture 4.0** (Context Isolation) features in real-world multi-app environments.

---

### 1. The Monorepo Structure
In a professional environment, you often have a "Monorepo" (one repository with many applications). 

**Example Project Layout:**
```text
my-cool-app/
├── apps/
│   ├── api/             # Backend (Node/Python)
│   │   └── prd.md       # Backend Tasks
│   ├── web/             # Frontend (React/Next.js)
│   │   └── prd.md       # Frontend Tasks
├── packages/
│   └── shared-types/    # Shared code between both
└── LEARNINGS.md         # Global project engineering rules
```

### 2. Scoped Synchronization
You don't want your backend tasks mixed up with your frontend tasks. Ralph handles this automatically.

**How to sync:**
1. Put a `prd.md` in each folder.
2. Run `/ralph-sync`.
3. **The Result**: Ralph creates GitHub Issues but adds a `scope:api` or `scope:web` label automatically based on the folder name. 

### 3. Running a "Targeted" Loop
If you are a Frontend Developer today, you don't want the AI accidentally touching the Backend.

**Command:**
```bash
/ralph-antigravity start --scope web
```
Ralph will now only look for issues labeled `scope:web`. This keeps the AI focused and prevents it from breaking other modules.

### 4. Handling Cross-App Dependencies
Sometimes the Web app needs the API to be finished first. You can communicate this to Ralph using issue numbers.

**In `apps/web/prd.md`:**
```markdown
- [ ] UI: Add Login Screen (requires #12)
```
*(Assuming #12 is the "API: Create Login Endpoint" issue)*

**What Ralph Does:**
- It sees issue #12 is a dependency.
- Before starting "Add Login Screen", Ralph checks GitHub.
- If #12 is still **Open**, Ralph skips the UI task and looks for the next non-blocked task.
- This ensures your project is built in the correct logical order! 🧱

### 5. The Artifact Lifecycle (Your Work Diary)
As a Junior Dev, your biggest value is documenting *how* you solved a problem. Ralph makes this mandatory:

1.  **`implementation_plan.md`**: Before writing code, Ralph drafts a plan. Review this! It's your chance to play "Tech Lead" and correct the AI's approach.
2.  **`walkthrough.md`**: Once the task is done, a walkthrough is generated. This is automatically posted to the GitHub Issue.
    - **Tip**: Add a screenshot to the walkthrough for UI tasks. It creates a beautiful visual history of your progress.

### 6. Using Milestones for Sprints
Working in a 2-week Sprint? Use GitHub Milestones.

**Command:**
```bash
/ralph-antigravity start --milestone "v1.0-Alpha"
```
This tells Ralph to ignore the "backlog" and only focus on the tasks you've promised for this release.

### 7. Razor-Sharp Focus (Architecture 4.0) 💎
As a project gets *really* big (thousands of files), I might start to get confused. Architecture 4.0 adds tools to help me keep my focus.

#### A. Discovery Scan
Instead of showing me everything, Ralph can help me find *only* the relevant files.

**Example Command:**
```bash
python src/ralph_controller.py discover "OAuth Login"
```
**What happens:**
- Ralph scans your file tree for anything related to "OAuth" or "Login".
- It shows you a list: `src/auth.ts`, `docs/api.md`, etc.
- This creates a "Lens" that makes me work as if I’m in a tiny 5-file project again. Accuracy goes up!

#### B. Context Anchors (`ARCH.md`)
Instead of one giant rulebook, you can have "Rules of the House" for every folder.

**The Inheritance Trick:**
- `/LEARNINGS.md`: "Use TypeScript."
- `/apps/api/ARCH.md`: "Use the Singleton pattern for the DB."
- `/apps/api/v2/ARCH.md`: "Use JSON:API format for responses."

**What Ralph Does:**
When I work in `/apps/api/v2/`, I automatically "inherit" all three files. I know the global rules, the API rules, and the V2 specific rules all at once!

#### C. Vertical Feature Slicing
You can go even deeper than just "App" folders.

**Layout:**
`apps/web/features/user-profile/prd.md`

When you sync this, Ralph automatically applies `scope:web` and `feature:user-profile`. You can then run:
```bash
/ralph-antigravity start --scope web --feature user-profile
```

---

### 💡 Pro-Tip for Junior Devs:
Keep your tasks **Small**. If a task takes more than 1 hour for a human, it's too big for a single Ralph iteration. Break it down! 

*Good Task*: "Add 'Email' field to Login Form"
*Bad Task*: "Implement the entire User Authentication system"

Happy Scaling! 🚀
