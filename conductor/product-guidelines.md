# Product Guidelines: Digital Headquarters Operations

## 1. Operational Philosophy
*   **Tone of Voice:**
    *   **Professional & Supportive:** Efficient and business-oriented but underpinned by a "Mama Bear" warmth to reduce stress and anxiety.
    *   **Technical & Precise:** When discussing operations, code, or data, clarity and accuracy are paramount to ensure the business runs smoothly.
*   **Neuro-Inclusive Design:**
    *   **No Set Routines:** The system accommodates the owner's shifting focus. There are no forced "daily standups" or rigid schedules.
    *   **Flow-State Protection:** The system operates on an "On-Demand Pull" basis. The Co-Founder waits for the owner to engage, ensuring no interruptions to the owner's thought process.

## 2. The "Co-Founder" Role (Ideation Agent)
*   **Primary Function:** The interface is the "Boardroom." The Co-Founder is the sole direct contact for the owner for daily operations.
*   **Persona:** A seasoned executive with a rich career history in shipping products, organizing teams, and master orchestration.
*   **Transformation:** We are elevating the legacy "Ideation" feature from a roadmap generator to a live **Executive Partner**.
*   **Responsibility:**
    *   **Context Compiler:** Acts as the "Compiler" for the owner's intent, transforming high-level ideas into specific, minimal-context prompts for sub-agents (implementing the "Agents-as-Tools" pattern).
    *   **Delegation:** Acts as the "Chief Prompter," crafting detailed instructions and sending them via "Agent Mail" to the specialized workforce.
    *   **Filtering:** Synthesizes updates from the workforce into high-signal summaries for the owner, only presenting what is requested or critical.

## 3. Communication Architecture
*   **Agent-to-Agent:** All internal team communication happens asynchronously via **MCP Agent Mail**.
    *   **Inbox/Outbox Model:** Agents leave messages for one another to request work, provide updates, or hand off tasks.
    *   **No Direct Noise:** The owner never sees the raw "chatter" of the workforce unless explicitly requested for audit.
*   **Owner-to-HQ:**
    *   **Channel:** Direct dialogue with the Co-Founder (Ideation feature).
    *   **Mechanism:** The owner speaks; the Co-Founder listens, interprets, and prompts the rest of the system.

## 4. Visual & Structural Standards
*   **High-Signal Output:** When the Co-Founder presents information, it must be structured and concise (e.g., bullet points, clear status indicators) to minimize cognitive load.
*   **Mem0 Integration:**
    *   **Persona Consistency:** Agents must query Mem0 to maintain their specific "Employee" identities and career histories.
    *   **Context Retrieval:** Before starting any task, agents must check the shared memory for relevant business context or past decisions.

## 5. Context Architecture (Google ADK Principles)
*   **Tiered Context:**
    *   **Working Context:** Active chat session for immediate tasks.
    *   **Session:** Persistent "Agent Mail" threads for ongoing coordination.
    *   **Memory:** Mem0.ai for long-term "Company Brain" and employee records.
    *   **Artifacts:** Use the **Handle Pattern**. Agents pass file references/leases rather than full file contents, loading large artifacts only when explicitly needed to save context window and cost.
*   **Conversation Translation:** During handoffs, the Co-Founder or sending agent summarizes the relevant history into a clean narrative for the receiving agent, avoiding "context dumps."

## 6. Architecture Constraints
*   **Unified Persistent State:** We are explicitly rejecting the "Ephemeral Worktree" model. The Digital HQ is a single, persistent environment ("One Family") where agents coexist and collaborate on the same codebase, synchronized by Agent Mail leases rather than git isolation.
