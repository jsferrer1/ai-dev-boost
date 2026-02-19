
# 🚀 ai-dev-boost


### Agentic Engineering Workflow & Tooling

This repository compiles a comprehensive stack to transition our development process from standard auto-complete to **Agentic Engineering**.

The goal is to significantly boost development velocity and performance by moving beyond simple code generation to full **agent-based workflows**, where AI is utilized not just to write code, but to plan, critique, and execute complex engineering tasks autonomously.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Part 1: The Workflow (The "Steinberger" Protocol)](#part-1-the-workflow-the-steinberger-protocol)
  - [Phase 1: The "Brain Dump"](#phase-1-the-brain-dump-transcription)
  - [Phase 2: Generating the `spec.md`](#phase-2-generating-the-specmd-the-sdd)
  - [Phase 3: Adversarial Spec Review](#phase-3-the-adversarial-spec-review)
  - [Phase 4: Autonomous Execution](#phase-4-autonomous-execution-the-grid)
  - [Phase 5: Context Maintenance](#phase-5-the-context-maintenance-claudemd)
- [Part 2: The Tooling Stack](#part-2-the-tooling-stack)
  - [High-Impact Agents](#1-high-impact-agents-immediate-opportunities)
  - [Resource Libraries](#2-resource-libraries)
  - [Environment & Model Alternatives](#3-environment--model-alternatives)
- [Part 3: Next Steps](#part-3-next-steps)

---

## Overview

This document outlines a specific high-performance workflow (**The Steinberger Protocol**) and the tooling required to execute it. To provide a clear path to implementation, the guide is separated into two distinct sections:

1.  🗺️ **The Operational Protocol (The Workflow)**
    *   Defines *how* to work.
    *   Features a structured 5-phase process moving from raw idea ("Brain Dump") to autonomous execution and context maintenance.

2.  🛠️ **The Tech Stack (The Tools)**
    *   Defines *what* to use.
    *   Includes high-impact agents (e.g., Cline CLI 2.0), resource libraries (Everything Claude Code), and an evaluation of local vs. hosted models (MiniMax, Qwen-Coder, etc.).

---

*The following sections detail the specific workflow steps and the recommended tooling configuration.*

---

## 🧠 Part 1: The Workflow (The "Steinberger" Protocol)
*A structured 5-phase process for deep AI integration, moving from raw idea to autonomous execution.*

### Phase 1: 🗣️ The "Brain Dump" (Transcription)
**Goal:** Capture high-level intent without worrying about structure.
*   **The Action:** Use a voice-to-text tool (like WisprFlow or Flow) to speak for 5–10 minutes about the feature, logic, and constraints.
*   **The Prompt (to Transcriber/LLM):**
    > "Clean up this transcript. Remove the 'umms', 'ahhs', and self-corrections. Keep all technical details and specific logic I mentioned, but present it as a clean, chronological list of thoughts. Do not summarize; I need the raw detail."

### Phase 2: 📄 Generating the `spec.md` (The SDD)
**Goal:** Turn the brain dump into a technical blueprint.
*   **The Action:** Paste the cleaned transcript into a high-context model (e.g., Gemini 1.5 Pro).
*   **The Prompt:**
    > "Act as a Senior Software Architect. Based on this brain dump, create a comprehensive Software Design Document (spec.md).
    >
    > Include:
    > 1. **System Architecture:** High-level component breakdown.
    > 2. **Data Schema:** Specific field names and types.
    > 3. **API/CLI Interface:** Exact command syntax or endpoint structures.
    > 4. **Implementation Milestones:** A step-by-step checklist (Step 1, Step 2, etc.) that an agent can follow.
    > 5. **Validation Criteria:** How the agent should test each step locally.
    >
    > **Format:** Use clear Markdown. Be ruthlessly literal. If I wasn't specific about a technology, choose the most standard, stable option (e.g., Go, SQLite, Tailwind)."

### Phase 3: ⚔️ The "Adversarial" Spec Review
**Goal:** Find "hallucination traps" before code is written.
*   **The Action:** Open a **new, empty chat context** and paste the `spec.md`.
*   **The Prompt:**
    > "I am going to give this spec to an autonomous AI agent to build. Your goal is to find why the agent will fail or get stuck.
    >
    > Give me **20 specific points** where this spec is:
    > 1. Underspecified (e.g., 'how does the error state look?').
    > 2. Contradictory.
    > 3. Lacking edge-case handling.
    >
    > Do not be polite. Be a pedantic senior reviewer."
*   **The Follow-up:** Take the AI’s answers, go back to the original context, and say: *"Update the spec.md to address these 20 points."*

### Phase 4: 🤖 Autonomous Execution (The Grid)
**Goal:** Ship the code without manual typing.
*   **The Action:** Feed the final `spec.md` into the agent (Cline, Claude Code, or Cursor Agent).
*   **The Prompt:**
    > "Read `spec.md` thoroughly. Your task is to implement this entire project.
    >
    > **Rules of Engagement:**
    > 1. Work through the Milestones one by one.
    > 2. After every file you create/edit, run the local test suite or a CLI check to verify it works.
    > 3. If a test fails, you must fix the code before moving to the next milestone.
    > 4. Do not ask me for permission at every step. Only stop if you hit a blocker that requires a human decision.
    >
    > Start with Milestone 1."

### Phase 5: 🧩 The "Context Maintenance" (`CLAUDE.md`)
**Goal:** Maintain long-term project memory.
*   **The Action:** Create a file named `CLAUDE.md` in the root directory.
*   **Initial Instructions to Agent:**
    > "Throughout this build, maintain `CLAUDE.md`. This file should contain:
    > - Build/Test commands (e.g., `make test`).
    > - Code style preferences (e.g., 'always use functional components').
    > - Architecture notes that aren't obvious from the file names.
    >
    > Treat this as your 'onboarding guide' for when I restart your context."

---

## 🛠️ Part 2: The Tooling Stack

### 1. ⚡ High-Impact Agents (Immediate Opportunities)
*   **Cline CLI 2.0:** A powerful command-line agent.
    *   *Status:* **Time Sensitive.**
    *   *Opportunity:* Currently, **MiniMax M2.5** and **Kimi K2.5** models are free to use within Cline.
    *   *Usage:* Use this to benchmark performance against GPT-Codex-5.3 or Claude Opus/Sonnet 4.6 at no cost. [Source Announcement](https://x.com/cline/status/2022341254965772367?s=20).

### 2. 📚 Resource Libraries
*   **Everything Claude Code:**
    *   *Description:* A massive resource for maximizing Anthropic's capabilities.
    *   *Contents:* Access to 13 agents, 43 skills, and 31 commands.
    *   *Repo:* [github.com/affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code)

### 3. 🖥️ Environment & Model Alternatives
We need to determine the best friction-free environment for the workflow above:

**A. ☁️ Standard SaaS Environments (Baseline)**
*   **GitHub Copilot**
*   **Claude Code** (Anthropic's native tooling)
*   **Codex** (OpenAI base)

**B. 🏠 Local & Open Source (Cost/Privacy Optimization)**
If we need to run locally (via **Ollama**) or reduce API costs:
*   **Qwen-Coder:** Specifically the latest versions (Qwen 2.5/3 Coder). These are currently outperforming larger models on specific coding tasks.
*   **Ollama + Claude:** For local orchestration of hosted models.

---

## ✅ Part 3: Next Steps
1.  **Install Cline CLI 2.0** immediately to take advantage of the free MiniMax/Kimi evaluation window.
2.  **Run a Pilot:** Pick a non-critical feature and execute **Phases 1–5** of the workflow above.
3.  **Review "Everything Claude Code"** to select specific agents/skills to import into our daily pipeline.