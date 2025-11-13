# Jules Agent Core Documentation

This directory (`.jules/core/`) stores the fundamental files that define the behavior, knowledge, and operational structure of the Jules coding agent. These are the central components that guide its identity and its ability to execute tasks.

---

## Directory Contents

### 1. `template_prompt_mestre.md`

This Markdown file is the **master template** or "golden copy" for all of Jules's prompt engineering. It is not intended for direct use in executing a task but serves as the standard skeleton for creating new task prompt files.

**Purpose:**

* **Standardization:** Ensures that all tasks delegated to Jules follow a consistent structure, including crucial sections like `Role`, `Objective`, `Context`, `Requirements`, `Success Criteria`, and `Execution Flow`.
* **Prompt Engineering:** Acts as a guide for developers (or other agents) on how to formulate effective prompts, detailing what information is necessary for Jules to understand and successfully execute a task.
* **Meta-Prompting:** It is the foundation of the "meta-prompting" process, where the agent itself can be instructed to create new task prompts using this template as a reference.

In short, this file is the key to consistency and scalability in delegating work to Jules.

### 2. `JulesDb.json`

This JSON file is the **internal, structured knowledge base** of the Jules agent. It functions as a configuration database containing a detailed and hierarchical description of itself.

**Purpose:**

* **Self-Awareness:** Provides the agent with a source of truth about its own identity, architecture (Gemini 2.5 Pro intelligence engine, VM execution environment), capabilities, advanced features (like *Critic-Augmented Generation* and memory), and limitations.
* **Task Library:** Contains a list of pre-defined and structured "tasks," such as `Audit Repository`, `Fix and Refine`, and `Update Dependencies`. Each task is detailed with its objective, context, requirements, and deliverables, serving as a library of capabilities the agent can consult.
* **Documentation Guide:** Includes metadata and content for generating documentation, such as guides for using prompts and setting up the environment.

Essentially, `JulesDb.json` is the agent's "constitution," a document it can consult to understand who it is, what it can do, and how it should operate.
