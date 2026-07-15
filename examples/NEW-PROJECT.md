# Practical Example: Starting a New Project from Scratch (Greenfield)

In a new project (0-to-1 Development), you have a blank canvas. While it's tempting to jump straight into coding, doing so with AI often leads to inconsistent architectures and hallucinated tech stacks. 

Spec-Driven Development (SDD) prevents this by forcing you to define the "What" and the "How" before any code is generated. This example demonstrates how to build a **"Photo Gallery App"** from scratch using our complete AI agent pipeline, ensuring a robust, scalable foundation.

---

## Step 1: Establishing the Foundation (The Constitution)
Since this is a blank repository, the Orchestrator needs to know your technological preferences and architectural rules. These rules will govern every AI agent in the pipeline.

**Action:** Open the VS Code Chat and invoke the orchestrator to set up the project rules.
> `@sdd Let's start a new project. Our stack is Next.js, TypeScript, and TailwindCSS. We strictly follow functional programming, use React Server Components where possible, and mandate Test-Driven Development (TDD) with Jest.`

**What happens:** The Orchestrator delegates to `@sdd.constitution`, which saves these rules in `.sdd/constitutions/constitution.md`. From now on, no agent will suggest using Python or Vue.js, as the stack is strictly locked.
👉 *(Button)* **Constitution defined. Ready to specify requirements?**

## Step 2: Visual & Functional Specification (Vision Capabilities)
Now we define what the application actually does. We will use VS Code's native Vision feature to let the AI see our UI wireframe.

**Action:** Click the handoff. **Drag and drop your UI mockup image** (e.g., a sketch of a photo grid with a sidebar) into the VS Code chat and type:
> `@sdd.specify Please use the attached mockup to write the functional specification and user stories for the "Photo Gallery" core feature. Users should be able to upload, tag, and view photos in a grid. Save the UI reference to the .sdd/ui/ folder.`

**What happens:** `@sdd.specify` analyzes the image, identifies the interactive elements (upload buttons, image grid, tags), writes the exact Acceptance Criteria in `.sdd/specs/`, and creates the local UI reference link.
👉 *(Button)* **Specification created. Ready to clarify requirements?**

## Step 3: Refinement (Preventing Hallucinations)
Even with a mockup, requirements can be ambiguous. The clarification phase forces the AI to ask you about edge cases before it plans the database.

**Action:** Click the handoff to trigger `@sdd.clarify`. 
*Agent asks:* "What is the maximum file size for a photo upload? And should tags be pre-defined or user-generated?"
*You reply:* "Max size is 5MB. Tags are user-generated, but should be converted to lowercase automatically."
👉 *(Button)* **Requirements clarified. Generate Wireflow?**

## Step 4: Visualizing the Navigation
**Action:** Click the handoff. `@sdd.wireflow` reads the spec and generates a Mermaid.js navigation diagram (e.g., Home -> Upload Modal -> Success State) and ASCII layouts in `.sdd/wireflows/`. This gives the upcoming planning agent a clear view of the routing structure.
👉 *(Button)* **Wireflow created. Ready for technical plan?**

## Step 5: Architectural Planning
**Action:** Click the handoff for `@sdd.plan`.
> `@sdd.plan Based on the clarified spec, create the technical architecture.`

**What happens:** The agent writes the `.sdd/plans/` document. Because it read the Constitution in Step 1, it correctly plans a Next.js Server Action for the upload endpoint and defines a generic `PhotoCard` React component using TailwindCSS.

## Step 6: Quality Gates (Checklists & Scenarios)
**Action:** Click the handoffs sequentially to build your testing foundation:
*   `@sdd.checklist` generates the "unit tests for English" (verifying if the spec has any logical holes).
*   `@sdd.qa-scenarios` writes the BDD/Gherkin test cases (e.g., *Given the user uploads a 6MB file, Then the system shows an error*).
👉 *(Button)* **QA Scenarios created. Generate tasks?**

## Step 7: Task Breakdown & GitHub Tracking
**Action:** Click the handoff for `@sdd.tasks`. Because our Constitution mandated TDD, the agent orders the tasks strictly: "Write Jest tests for upload logic" comes *before* "Implement upload logic".
👉 *(Button)* **Tasks generated. Export to issue tracker?**

**Action:** Click the handoff. `@sdd.taskstoissues` leverages the `#tool:github/create_issue` MCP server to push these generated tasks into your team's live GitHub repository.
👉 *(Button)* **Issues created. Run consistency analysis?**

## Step 8: Initial Implementation
**Action:** Run `@sdd.analyze` to confirm everything is perfectly aligned. Then start coding:
> `@sdd.implement The artifacts are consistent. Please execute the tasks to build the Photo Gallery.`

**What happens:** The agent uses its terminal to install Next.js, creates the folder structure, writes the tests, and implements the code.
👉 *(Button)* **Implementation complete. Run convergence check?**

## Step 9: The Convergence Loop (The SDD Safety Net)
Even in a greenfield project, the AI might miss a detail during its first implementation pass (e.g., it built the upload logic but forgot the lowercase conversion for tags).

**Action:** Click the handoff to run the convergence check.
> `@sdd.converge Please assess the codebase against our spec and plan to verify if all planned work is complete.`

**What happens:** 
The `@sdd.converge` agent acts as your auditor. It cross-references the generated code with your `.sdd/specs/` and `.sdd/plans/`. 
If it realizes the tag lowercasing logic or the 5MB file limit validation was forgotten, **it will automatically append those missing items as new tasks to your `.sdd/tasks/` file**.

If the command appends new tasks, simply click the handoff to run `@sdd.implement` again to execute those specific fixes. Repeat the `@sdd.converge` step until the agent reports that the feature has fully converged and matches the specification 100%.
