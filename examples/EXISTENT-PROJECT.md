# Practical Example: Adding a Feature to an Existing Project (Brownfield)

In legacy or existing projects, context is everything. The key to success in Spec-Driven Development (SDD) is using "Context Engineering" — deliberately feeding the AI information about your current architecture before writing new code. By leveraging VS Code's native variables like `#codebase` and `#file`, you ensure the agents hook into the current architecture without reinventing the wheel or breaking existing patterns.

In this highly detailed example, we will add a **"Comment System"** to an existing Kanban board application (Taskify).

---

## Step 1: Reverse Engineering the Constitution (Context Engineering)
Before building, we need the Orchestrator to understand our legacy rules. In existing projects, the Constitution acts as a strict guardrail to prevent the AI from introducing foreign libraries or conflicting architectural patterns.

**Action:** Open the VS Code Chat and invoke the orchestrator, forcing it to scan the current state of the project.
> `@sdd Please analyze my #codebase and create the project constitution. Maintain the current architectural patterns. Crucial rule: Always reuse existing UI components from our design system (like the Button and Modal components in #file:src/components/ui) instead of creating new ones. We use Prisma for the DB and Tailwind for styling.`

**What happens:** The agent scans your workspace and creates `.sdd/constitutions/constitution.md`. It formally records your existing tech stack, UI library, and database ORM as immutable rules for all subsequent subagents.
👉 *(Button)* **Constitution defined. Ready to specify requirements?**

## Step 2: Specification with Vision Capabilities
We want to add a comment section to the existing Task Modal. Instead of just describing it, we will show the AI what the current modal looks like.

**Action:** Click the handoff. **Drag and drop a screenshot** of the current Task Modal into the VS Code chat (leveraging the Vision feature) and type:
> `@sdd.specify I want to add a comment system for Kanban tasks. I'm attaching a screenshot of our current Task Modal with my sketch of the new comment timeline at the bottom. Please write the user stories and acceptance criteria. Save the UI reference in the .sdd/ui/ folder.`

**What happens:** The agent analyzes the layout, identifies where the new comments fit into the legacy UI, writes the spec in `.sdd/specs/`, and creates the image reference link.
👉 *(Button)* **Specification created. Ready to clarify requirements?**

## Step 3: Refinement Against Legacy Code
In an existing project, new features must map to existing database tables and models. The clarification phase is where we bridge the gap between the new spec and the old schema.

**Action:** Click the handoff for `@sdd.clarify`. 
*Agent asks:* "Does the system already have a concept of a `User` to attribute these comments to, and where is the `Task` stored?"
*You reply:* "Yes, we have an existing `User` and `Task` table. Please review the schema in `#file:prisma/schema.prisma` and ensure the new `Comment` model establishes relations with them."
👉 *(Button)* **Requirements clarified. Generate Wireflow?**

## Step 4: Visual & State Mapping
**Action:** Click the handoff. `@sdd.wireflow` generates Mermaid.js diagrams mapping how the user interacts with the legacy Task Modal to post a comment, generating ASCII representations of the UI states in `.sdd/wireflows/`.
👉 *(Button)* **Wireflow created. Ready for technical plan?**

## Step 5: Legacy-Focused Architectural Planning
This is the most critical phase for Brownfield projects. The technical plan must explicitly detail how existing files will be modified.

**Action:** Click the handoff for `@sdd.plan`.
> `@sdd.plan Create the technical plan. IMPORTANT: Review our `#codebase` to integrate the new comments table with the existing Prisma schema. The plan must list exactly which existing React components (e.g., `#file:src/components/TaskModal.tsx`) will be modified.`

**What happens:** The agent writes the `.sdd/plans/` document, detailing the exact diffs and dependency injection required to add comments without breaking the existing Kanban drag-and-drop features.

## Step 6: Quality Gates & Regression Protection
**Action:** Click the handoffs sequentially to generate quality control documents:
*   `@sdd.checklist` generates the acceptance checklist, specifically adding regression checks (e.g., "Verify that adding a comment does not prevent the task from changing columns").
*   `@sdd.qa-scenarios` writes the BDD/Gherkin tests for the QA team, factoring in existing test utilities.
👉 *(Button)* **QA Scenarios created. Generate tasks?**

## Step 7: Task Breakdown & GitHub Tracking
**Action:** Click the handoff for `@sdd.tasks`. It creates a step-by-step TDD sequence, carefully separating "Modify existing Schema" from "Update existing UI".
👉 *(Button)* **Tasks generated. Export to issue tracker?**

**Action:** Click the handoff. `@sdd.taskstoissues` uses the `#tool:github/create_issue` MCP server to push these granular tasks into your team's live Jira/GitHub board so product managers have full visibility.
👉 *(Button)* **Issues created. Run consistency analysis?**

## Step 8: Safe Implementation
**Action:** Run `@sdd.analyze` to cross-audit the plan against the legacy files. Once approved, start coding:
> `@sdd.implement The artifacts are consistent. Please execute the tasks. Use caution when applying diffs to our existing files like `#file:src/components/TaskModal.tsx`.`

**What happens:** The agent uses its terminal and file editing tools to safely modify your legacy files. 
👉 *(Button)* **Implementation complete. Run convergence check?**

## Step 9: The Convergence Loop (The SDD Safety Net)
In legacy codebases, the first implementation pass almost never catches 100% of the required integrations. The `@sdd.converge` agent acts as your ultimate quality gate. It assesses the current codebase against the feature's specifications, plans, and tasks to ensure no planned work was left behind [1, 2].

**Action:** Click the handoff to run the convergence check.
> `@sdd.converge Please assess the codebase against our spec and plan to verify if all planned work is complete.`

**What happens:** 
If the agent finds that the new comment system caused the legacy modal to lose its maximum height property, or missed a database migration, **it will automatically append a bug-fix or missing task to your `.sdd/tasks/` file**.

If the command appends new tasks, you must click the handoff to run `@sdd.implement` again to execute those specific fixes, and then repeat the `@sdd.converge` step [2, 3]. You loop through these two agents until `@sdd.converge` reports that the feature is fully complete and perfectly aligned with the specification.