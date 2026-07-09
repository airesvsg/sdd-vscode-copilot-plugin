# Practical Example: Adding a New Feature to an Existing Project (Brownfield)

In existing projects, Spec-Driven Development focuses on "Iterative Enhancement". The key to success here is ensuring that the AI agents read the current codebase and respect the existing architecture before planning and coding.

In this example, we will add a **"Comment System"** to our existing Taskify app.

---

## Step 1: Contextualization and Constitution (Update)
**Action:** If your project already has a constitution at `.sdd/constitutions/constitution.md`, you can skip this step. If not, you need to create it by asking the agent to read your current project.

**You type in the chat (using the `#codebase` or `#workspace` context variable):**
> `@sdd This is an existing project. Please analyze my #codebase and create the project constitution. Maintain the current architectural patterns (React on the frontend, Node.js on the backend). Add the rule: "Always reuse existing UI components instead of creating new ones."`

**What the agent does:**
It generates the constitution based on your current code and suggests the handoff:
👉 *(Button)* **Constitution defined. Ready to specify requirements?**

---

## Step 2: Specifying the New Feature
**Action:** Click the suggested handoff button. It is time to focus on the "What" and "Why" of the new feature, without focusing on the tech stack.

**You complete the prompt in the chat:**
> `@sdd.specify I want to define the functional specification and user stories. Here is what I want to build: A comment system for Kanban tasks. Users should be able to open an existing task, type a comment of up to 500 characters, see the comment's date/time, and see who wrote it.`

**What the agent does:**
It creates the `.sdd/specs/0002-task-comments-system.md` file (assuming `0001` was the initial creation of the app).
👉 *(Button)* **Specification created. Ready to clarify requirements?**

---

## Step 3: Refinement (Crucial for Existing Projects)
**Action:** For legacy or existing codebases, always click this handoff. `@sdd.clarify` will ask vital questions about how the new feature integrates with what already exists.

**You click the button:**
> `@sdd.clarify Please read the newly created specification and raise questions...`

**The agent might ask:**
*"How will we link the comment's author? Is there already a user authentication system and a `users` table in the current database?"*

**You reply in the chat:**
> `Yes, we already have a 'users' table in the database and an authentication context on the frontend (useAuth). Comments cannot be edited, only deleted by their own author.`

It updates the spec with your answers and suggests:
👉 *(Button)* **Requirements clarified. Ready to create the technical plan?**

---

## Step 4: Legacy-Focused Technical Planning
**Action:** Click the handoff button. **Attention here:** you must instruct `@sdd.plan` to verify the local code so it doesn't duplicate what already exists.

**You complete the prompt in the chat:**
> `@sdd.plan Based on the clarified specification, please create the technical implementation plan. My tech stack is: React and Node.js. IMPORTANT: Review our current database models and existing UI components to integrate them with the new comments table.`

**What the agent does:**
It reads the specification and the project's code, creating `.sdd/plans/0002-task-comments-system-plan.md` focused on how to connect the new feature to the existing architecture.
👉 *(Button)* **Technical plan created. Generate quality checklist?**

---

## Step 5: Generating the Quality Checklist
**Action:** Click the handoff button.
> `@sdd.checklist Based on the specification and the technical plan just created, please generate a comprehensive quality and validation checklist.`

**What the agent does:**
Generates `.sdd/checklists/0002-task-comments-system-checklist.md` containing regression tests (to ensure adding comments didn't break the existing Kanban board) and acceptance criteria.
👉 *(Button)* **Quality checklist created. Generate tasks?**

---

## Step 6: Actionable Task Breakdown
**Action:** Click the handoff button.
> `@sdd.tasks Using the technical plan and the quality checklist, please generate an actionable, sequential task list for implementation.`

**What the agent does:**
Generates `.sdd/tasks/0002-task-comments-system-tasks.md`. Tasks will include steps like "Modify existing routes" or "Update the `TaskModal.tsx` component", directly handling the real codebase.
👉 *(Button)* **Tasks generated. Run consistency analysis?**

---

## Step 7: Consistency Analysis
**Action:** Click the handoff button.
> `@sdd.analyze Please run a cross-artifact consistency analysis...`

**What the agent does:**
Checks for gaps (e.g., verifying if the plan included the foreign key to the existing `users` table that we agreed on during the Clarify step).
👉 *(Button)* **Analysis complete. Start implementation?**

---

## Step 8: Safe Implementation
**Action:** Click the handoff to trigger `@sdd.implement`.

**You click the button:**
> `@sdd.implement The artifacts are consistent and aligned. Please begin executing the tasks sequentially...`

**What the agent does:**
It will execute the code. Because it is an existing project, it will read legacy files (like your `TaskModal.tsx`), apply diffs, and run `npm install` in the terminal if any new library was planned.
👉 *(Button)* **Implementation complete. Run convergence check?**

---

## Step 9: Review and Convergence
**Action:** Click the handoff button.
> `@sdd.converge Please assess the current codebase against the feature's artifacts...`

**What the agent does:**
It verifies the newly made code edits. It might notice, for example, that the Kanban modal visually breaks when loading too many comments. If anything is pending, it will edit `.sdd/tasks/0002-task-comments-system-tasks.md` by adding fine-tuning tasks and will suggest running the implementation once more.

---

### Extra Tips for Existing Projects:
* **Context is King:** AI tools in existing codebases often fail when reinventing the wheel. If the agent tries to create a new button, warn it in the Planning step (Technical Plan) to use the existing button component from your local Design System.
* **Context Engineering:** Maintain files like `ARCHITECTURE.md` or rules in `.github/copilot-instructions.md` at the root of your project. The agents will read these files automatically to make better architectural and implementation decisions.
