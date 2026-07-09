# Spec-Driven Development (SDD) Agent Plugin for VS Code

This plugin brings the **Spec-Driven Development (SDD)** methodology natively to the Visual Studio Code chat. It utilizes the native **Agent Plugins (Preview)** feature to orchestrate specification-driven software development.

Spec-Driven Development inverts the traditional process: instead of jumping straight into code, **specifications become the primary, executable artifact**. You define "what" to build, refine the requirements through structured phases, and allow the AI agent in VS Code to implement the solution.

## 🚀 How to Install the Plugin

This workflow is distributed as a VS Code Agent Plugin. You can install it directly from this Git repository URL:

1. Open Visual Studio Code.
2. Open the *Command Palette* (`Ctrl+Shift+P` on Windows/Linux or `Cmd+Shift+P` on macOS).
3. Type and select the command: **Chat: Install Plugin From Source**.
4. Paste the URL of this Git repository (e.g., `https://github.com/airesvsg/sdd-vscode-copilot-plugin`) and press Enter.

VS Code will clone and install the plugin, activating it automatically in your chat environment. 

> **Note:** Make sure the `chat.plugins.enabled` setting is set to `true` in your VS Code, as this is a Preview feature.

---

## 🏗️ Agent Architecture

The workflow uses an "Orchestrator and Experts" pattern. Navigation between phases is guided by **Handoffs**, which allow a seamless transition in the VS Code chat from one specialized agent to another with a single click and a pre-filled prompt.

### The Coordinating Agent: `@sdd`
The main agent and the only one directly invocable by the user. It acts as the Orchestration Lead, guiding the user through the project lifecycle and delegating work to the appropriate subagents via the `agents` property in the frontmatter. **The coordinator never writes code; its function is to manage the workflow.**

### The Expert Subagents
Each step is mapped to a focused subagent with restricted permissions (such as read-only access) operating behind the scenes:

*   🛡️ **`sdd.constitution`:** Establishes the fundamental project rules and technology preferences (saves to `.sdd/constitutions/`).
*   📝 **`sdd.specify`:** Focuses on the "What" and "Why". Generates a requirements document with user stories (saves to `.sdd/specs/`).
*   🔍 **`sdd.clarify`:** Analyzes the specification to identify underspecified areas and asks questions before planning.
*   📐 **`sdd.plan`:** Provides the "How". Combines the specification with the tech stack to create the architecture (saves to `.sdd/plans/`).
*   ✅ **`sdd.checklist`:** Generates "unit tests for English," ensuring requirements are clear and consistent (saves to `.sdd/checklists/`).
*   📋 **`sdd.tasks`:** Transforms the plan into a sequential task list for development (saves to `.sdd/tasks/`).
*   🎫 **`sdd.taskstoissues`:** Converts the generated task lists into your project tracker (e.g., GitHub Issues) for execution visibility.
*   🕵️ **`sdd.analyze`:** Cross-audits artifacts to ensure perfect alignment before coding.
*   💻 **`sdd.implement`:** The only subagent with editing permissions and access to VS Code's integrated terminal. Strictly executes tasks, generating code and tests.
*   🔄 **`sdd.converge`:** Evaluates the generated code against the original specification and appends any pending items as new tasks.

---

## 🎯 How to Use the Workflow

Manual work is minimized through **Handoffs**, interactive buttons that appear at the end of each response, transferring context to the next agent in VS Code.

1. **Open the VS Code Chat** and call the coordinating agent with `@sdd`.
2. **Define the Constitution (If it is a new project):**
   `@sdd Let's establish the project rules. We use TypeScript, Next.js, functional approaches, and testing with Jest.`
3. **Start the Specification:**
   `@sdd I want to create an app to organize my photos into albums by date.`
4. **Follow the Handoffs:** The chat will suggest transition buttons to create guided sequential workflows. Just click them to advance:
   *   *Constitution defined. Ready to specify requirements?*
   *   *Specification created. Ready to clarify requirements?*
   *   *Requirements clarified. Ready to create the technical plan?*
   *   *Technical plan created. Generate quality checklist?*
   *   *Quality checklist created. Generate tasks?*
   *   *Tasks generated. Export to issue tracker?*
   *   *Issues created. Run consistency analysis?*
   *   *Analysis complete. Start implementation?*
   *   *Implementation complete. Run convergence check?*

At the end, if the `@sdd.converge` agent finds gaps and adds new tasks, click the button to run the implementation again until the feature is 100% compliant with the plan.

---

## 🔧 Updating the Plugin

When our team releases new improvements for the agents, you can quickly update your local version:
1. Open the VS Code Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`).
2. Run the command **Extensions: Check for Extension Updates**.
VS Code will automatically pull the changes from our Git repository and update the agents in your environment.

## 💡 Credits & Inspiration

This plugin is heavily inspired by **[Spec Kit](https://github.com/github/spec-kit)**, an open-source toolkit created by GitHub to help developers get started with Spec-Driven Development. 

While the original Spec Kit provides a CLI and works across multiple coding agents using slash commands, this plugin adapts its core philosophy (Spec → Plan → Tasks → Implement) into a fully native **VS Code Agent Plugin**. It leverages VS Code's Custom Agents and interactive Handoffs to create a seamless, UI-driven orchestration experience.