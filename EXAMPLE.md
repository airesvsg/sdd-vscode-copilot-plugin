# Practical Example: Building "Taskify" with Spec-Driven Development (SDD)

This document demonstrates an end-to-end flow in the VS Code chat using our SDD agent plugin. The goal is to build **Taskify**, a team productivity platform.

The process requires you to use the *Handoff* buttons suggested by Copilot at the end of each step to maintain a fluid context, seamlessly transitioning information between the expert subagents.

---

## Step 1: Establishing the Constitution (Project Rules)
**Action:** Open the VS Code chat and start the project by invoking the main orchestrator and defining the base rules.

**You type in the chat:**
> `@sdd Let's start the Taskify project. Define the project constitution. Our principles are: mobile-first, accessibility first, and test-driven development (TDD). The tech stack will be React, Node.js, and PostgreSQL.`

**What the agent does:**
The orchestrator delegates this to the `@sdd.constitution` subagent. It uses the edit tool to create the `.sdd/constitutions/constitution.md` file containing these rules. Once finished, it suggests the handoff button:
👉 *(Button)* **Constitution defined. Ready to specify requirements?**

---

## Step 2: Creating the Functional Specification (What and Why)
**Action:** Click the suggested handoff button. This will call the `@sdd.specify` subagent. You just need to complete the prompt with your business requirements.

**You complete the prompt in the chat:**
> `@sdd.specify I want to define the functional specification and user stories. Here is what I want to build: An app called Taskify. It should allow users to create Kanban boards, add tasks with titles and descriptions, and move these tasks between columns (To Do, In Progress, Done).`

**What the agent does:**
It analyzes the requirements and creates the `.sdd/specs/0001-taskify-kanban-board.md` file containing the user stories. Once finished, it suggests the handoff:
👉 *(Button)* **Specification created. Ready to clarify requirements?**

---

## Step 3: Refinement and Disambiguation
**Action:** Click the handoff button to call `@sdd.clarify`. NEVER skip this step for real projects.

**You click the button (the prompt is sent automatically):**
> `@sdd.clarify Please read the newly created specification and raise questions about ambiguities, edge cases...`

**What the agent does:**
It reads the specification located in `.sdd/specs/` and asks questions in the chat (e.g., *"What happens if the user tries to move a task to a column that doesn't exist?"* or *"Will there be a character limit on the task title?"*).

**You reply in the chat:**
> `1. Columns are fixed, no new ones can be created right now. 2. The title limit is 100 characters.`

It will update the specification (`.sdd/specs/0001-taskify-kanban-board.md`) by appending a `## Clarifications` section and then suggest the handoff:
👉 *(Button)* **Requirements clarified. Ready to create the technical plan?**

---

## Step 4: Technical Planning (The How)
**Action:** Click the handoff button to trigger `@sdd.plan`. You must confirm your technology stack.

**You complete the prompt in the chat:**
> `@sdd.plan Based on the clarified specification, please create the technical implementation plan. My tech stack is: React (Frontend), Node.js/Express (Backend), and PostgreSQL (Database).`

**What the agent does:**
It cross-references the specification with the constitution and your chosen tech stack to generate the architecture. It creates the `.sdd/plans/0001-taskify-kanban-board-plan.md` file and suggests:
👉 *(Button)* **Technical plan created. Generate quality checklist?**

---

## Step 5: Generating the Quality Checklist
**Action:** Click the handoff button. This calls `@sdd.checklist` to create your validation criteria.

**You click the button (the prompt is sent automatically):**
> `@sdd.checklist Based on the specification and the technical plan just created, please generate a comprehensive quality and validation checklist.`

**What the agent does:**
It creates the `.sdd/checklists/0001-taskify-kanban-board-checklist.md` file, which contains rigorous test scenarios and acceptance criteria based on both the plan and the specification.
👉 *(Button)* **Quality checklist created. Generate tasks?**

---

## Step 6: Actionable Task Breakdown
**Action:** Click the handoff button to call `@sdd.tasks`, which will create the execution roadmap.

**You click the button (the prompt is sent automatically):**
> `@sdd.tasks Using the technical plan and the quality checklist, please generate an actionable, sequential task list for implementation.`

**What the agent does:**
It creates the `.sdd/tasks/0001-taskify-kanban-board-tasks.md` file, outlining the exact sequence of implementation (e.g., 1. Database models, 2. API endpoints, 3. UI Components).
👉 *(Button)* **Tasks generated. Run consistency analysis?**

---

## Step 7: Consistency Analysis (Audit)
**Action:** Click the handoff button. `@sdd.analyze` will perform a cross-artifact safety check before any code is written.

**You click the button (the prompt is sent automatically):**
> `@sdd.analyze Please run a cross-artifact consistency analysis to ensure the specs, plans, checklists, and tasks align perfectly...`

**What the agent does:**
It reads the files across all directories (`.sdd/constitutions/`, `.sdd/specs/`, `.sdd/plans/`, `.sdd/checklists/`, and `.sdd/tasks/`) without modifying them. It outputs a report in the chat notifying you if any dependencies were missed (e.g., *"All clear! The tasks cover 100% of the specification and respect the TDD approach required in the constitution."*).
👉 *(Button)* **Analysis complete. Start implementation?**

---

## Step 8: Implementation (Hands-on)
**Action:** It's time to write code! Click the handoff to trigger `@sdd.implement`.

**You click the button (the prompt is sent automatically):**
> `@sdd.implement The artifacts are consistent and aligned. Please begin executing the tasks sequentially...`

**What the agent does:**
It will now use real tools (`edit` and `terminal`). It reads the `.sdd/tasks/0001-taskify-kanban-board-tasks.md` file and follows the tasks strictly: it will create the test files first (since TDD was required in the constitution), then the API code, and finally the React components. It will execute actual edits within your project. Once it finishes these steps, it suggests:
👉 *(Button)* **Implementation complete. Run convergence check?**

---

## Step 9: Review and Convergence
**Action:** After the coding phase, ensure no requirements were left behind by triggering `@sdd.converge`.

**You click the button (the prompt is sent automatically):**
> `@sdd.converge Please assess the current codebase against the feature's artifacts...`

**What the agent does:**
It compares the actual code generated in your project against the acceptance criteria and checklists.
- **Scenario A:** If something is missing (e.g., error handling when deleting a task), it edits the `.sdd/tasks/0001-taskify-kanban-board-tasks.md` file to append the missing tasks and suggests a handoff button to route back to `@sdd.implement`.
- **Scenario B:** If everything perfectly aligns, it declares convergence has been achieved: *"Convergence Achieved. The feature is complete and ready for delivery."*
