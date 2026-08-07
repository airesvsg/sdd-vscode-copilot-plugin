# Spec-Driven Development (SDD) Agent Plugin for VS Code

Build high-quality software by making **specifications the primary, executable artifact** of your development lifecycle. Inspired by the [Spec Kit](https://github.com/github/spec-kit) methodology, this plugin transforms Visual Studio Code into a guided SDD pipeline where AI agents handle requirements, planning, and implementation with strict architectural discipline.

## 📝 Summary

The **SDD Agent Plugin** is a comprehensive orchestration framework that replaces "vibe coding" with a structured, step-by-step process. By using a single lead orchestrator (`@sdd`) and a team of internal expert subagents, it ensures that every line of code is anchored to a verified functional requirement.

## 🌟 Key Highlights
*   **Orchestrated Workflow:** Interact only with the lead agent `@sdd`. It delegates tasks to specialized subagents (Product Manager, Architect, QA, Implementer) that are hidden from the main menu to reduce clutter.
*   **Vision-Powered Specs:** Drag and drop UI mockups directly into the chat. The agents analyze visual layouts to extract precise acceptance criteria.
*   **Permanent Traceability:** Every file modified by the plugin includes a mandatory header log linking the code to its governing specifications.
*   **Safety & Quality Gates:** Built-in loops for requirements clarification, BDD test scenario generation, and a final "Convergence" check to ensure implementation matches intent 100%.

## 🛣️ The SDD Lifecycle

The plugin guides you through a sequential flow using **Native Handoffs**. You simply follow the buttons provided by the agents:

1.  **Constitution:** Define the "immutable" tech stack and architectural rules.
2.  **Specify:** Define the "What" and "Why" (User Stories & Acceptance Criteria).
3.  **Clarify:** Identify and resolve ambiguities before any planning starts.
4.  **Wireflow:** Visualize navigation and UI states.
5.  **Plan:** Design the technical architecture and database schemas.
6.  **Checklist:** Generate a "Definition of Done" for the requirements.
7.  **QA Scenarios:** Translate requirements into BDD/Gherkin test cases.
8.  **Tasks:** Break the plan into a sequential, TDD-focused task list.
9.  **Implement:** Autonomous code generation with terminal execution and file editing.
10. **Converge:** The ultimate audit. Compares code against specs and generates fix-up tasks for any gaps.

## 🤖 The Expert Subagents (Internal)

These agents are orchestrated by `@sdd` and are not directly invocable by users to maintain process integrity:

*   📜 **`sdd.constitution`:** Establishes the foundation in `.sdd/constitutions/`.
*   🎯 **`sdd.specify`:** Analyzes Vision mockups and writes specs in `.sdd/specs/`.
*   🔍 **`sdd.clarify`:** Acts as a Senior BA to quiz the user on edge cases.
*   📐 **`sdd.plan`:** Creates the technical blueprint in `.sdd/plans/`.
*   🧪 **`sdd.qa-scenarios`:** Writes BDD tests in `.sdd/qa-scenarios/`.
*   ⚙️ **`sdd.implement`:** Executes tasks and maintains file traceability.
*   🏁 **`sdd.converge`:** The "Safety Net" that loops implementation until the feature is complete.

## 🚀 Practical Examples

### 1. Greenfield Project (Starting from Scratch)
*   **Step 1:** `@sdd Let's start a new project. Stack: Next.js, TypeScript, Tailwind.`
*   **Step 2:** Drag your UI sketch into chat: `@sdd Specify this "Photo Gallery" feature using the attached image.`
*   **Step 3:** Follow the **Handoff Buttons** through Planning, QA, and Implementation.
*   **Step 4:** Run the **Convergence Check** to ensure the AI didn't miss specific logic like image size limits.

### 2. Brownfield Project (Existing Codebase)
*   **Step 1:** `@sdd Analyze my #codebase and create a constitution based on our existing patterns.`
*   **Step 2:** Provide context: `@sdd Specify a new "Comment System" for our Kanban board. See #file:src/db/schema.prisma for reference.`
*   **Step 3:** The `sdd.plan` agent will specifically look at your current files to avoid duplicating code.
*   **Step 4:** Implementation will use **Traceability Headers** to log which spec updated which legacy file.

## 🔗 Traceability & Maintenance

To ensure the level of maturity required for professional SDD, the `sdd.implement` agent follows a strict **File Header Rule**. Every file created or modified will contain or append to this block:

```javascript
/* SDD - vscode copilot plugin
 *
 * Specs
 * ------------------
 * - 0001-initial-setup.md
 *   02/03/2026 10:15:00
 * - 0003-comment-system.md
 *   05/04/2026 14:20:00
 */
```
This allows the `@sdd.converge` agent to always know which requirements define the current state of a file.

---

## 🖼️ Handling UI Designs and Mockups

When building frontend features, Spec-Driven Development works best with a hybrid approach combining file-based documentation and VS Code's native Vision capabilities:

1. **Document (The SDD Way):** Save your UI mockups or screenshots in a dedicated directory, such as `.sdd/ui/0001-feature-name-ui.png`. This keeps visual assets version-controlled and tied to your feature specification.
2. **Reference:** Link the image inside your Markdown specification or wireflow files (e.g., `![UI Mockup](../../.sdd/ui/0001-feature-name-ui.png)`).
3. **Attach in Chat (Vision):** LLMs cannot automatically "see" local images just by reading a file path. When you invoke `@sdd.specify` to write user stories, or `@sdd.implement` to write code, **drag and drop the image directly into the VS Code chat box**. This leverages the Vision feature, allowing the agent to analyze the layout, colors, and structure instantly while recording the reference in your SDD artifacts.


## 💰 Token Economy & Cost Optimization

To maximize the efficiency of your AI credits, follow these strategic guidelines:

1.  **Context Isolation:** Perform planning and implementation in separate chat sessions to prevent "context dumping" that confuses the AI.
2.  **Precise Targeting:** Use specific file references (`#file`) instead of global codebase scans (`#codebase`) whenever possible.
3.  **Prompt Caching:** Agent instructions are placed at the **top** of the files to increase "cache hit" rates in VS Code, reducing latency and cost.
4.  **Phased Implementation:** For large features, implement in small increments (e.g., Database first, then Logic, then UI). This keeps prompts short and accurate.

## 🛠️ Installation

1.  Open the Command Palette (**Ctrl+Shift+P**).
2.  Run `Chat: Install Plugin From Source`.
3.  Enter the URL of this repository.
4.  Type `@sdd` in the Chat View to begin.

> **Note:** Make sure the `chat.plugins.enabled` setting is set to `true` in your VS Code, as this is a Preview feature.

---
*Inspired by [Spec Kit](https://github.com/github/spec-kit). Build intent, not just code.*
