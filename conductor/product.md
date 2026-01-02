# Initial Concept
I want to be able to basically create employees to help me run my business. I've got autism and ADHD, and I need all the help I can get. Who more would someone like me need than a team of models rather than a team of humans? We're going to create a system where just by me talking to one model, she can communicate back and forth with all my other models. Some will be hosted on Azure endpoints, which I'll handle system prompts on that side. However, this application will need to connect to the Azure agent platform, which is SSE and HTTP streamable MCP tools that I can add into Azure DirectLink, so we'd need a way to host that.

Initially, among their normal agents within this, I'm also going to be creating employees—real history, career history-based employees—to help me run my business along with other CLI tools. Like yourself and Claude, they're coming from a variety of different platforms and endpoints.

# Product Guide: Digital Workforce Headquarters

## 1. Vision & Mission
**Vision:** To create a "Digital Company Headquarters" that serves as the central nervous system for a multi-agent workforce. This system will empower the owner (Nathan) by managing cognitive load and orchestrating a team of autonomous AI "employees" with distinct personalities, memories, and career histories.

**Mission:** To provide a unified, persistent coordination layer where agents from diverse platforms (Azure Foundry, Gemini CLI, AutoClaude) can communicate, collaborate, and execute workflows asynchronously, acting as a cohesive team rather than isolated tools.

## 2. Core Users
*   **The Owner (Nathan):** The CEO needing high-level orchestration, ideation support, and a reduction in executive function overhead.
*   **The "Employees" (Agents):**
    *   **Ideation Partner:** The primary interface for brainstorming and planning.
    *   **Azure Foundry Agents:** Specialized agents hosted on Azure with specific system prompts and knowledge bases.
    *   **CLI Agents:** Local agents (Gemini, Claude Code) performing execution tasks.
    *   **AutoClaude:** The autonomous execution engine acting as the physical "office" for code work.

## 3. Key Capabilities & Features
### A. The "Digital HQ" (Coordination Layer)
*   **Unified Inbox/Outbox:** A central message bus where all agents send updates, requests, and handovers.
*   **Identity & Persona Management:** Storage for "Employee Records"—rich bios, career histories, and evolving resumes that give agents persistent context and personality.
*   **Context Continuity:** Searchable history ensuring no context is lost between sessions or tools.

### B. Enterprise Memory Infrastructure (Mem0)
*   **Mem0 Cloud Enterprise:** Utilization of the enterprise-grade memory layer for robust, long-term, and scalable memory management.
    *   **Global Company Brain:** A unified memory pool accessible by all agents (local and cloud) via Mem0's Enterprise API/MCP.
    *   **Persistent Employee Growth:** Mem0 will track the professional growth, decisions, and relationship context for every "employee" agent.
*   **Agent Guardian:** A dedicated role overseeing memory integrity and ensuring agents stay "in character" and adhere to business goals, leveraging the high availability of the enterprise memory tier.

### C. Azure & Cloud Integration
*   **Azure DirectLink Compatibility:** The system must expose SSE/HTTP streamable endpoints to function as a native tool within Microsoft Foundry.
*   **Public Hosting:** Deployment to a robust cloud provider (Railway, Cloud Run, or similar) to ensure the API is accessible to Azure agents 24/7.
*   **Security:** Handling of server-side and client-side credentials to securely bridge local context with cloud agents.

### D. Workflow Automation
*   **Message-Triggered Workflows:** The ability to "email" an agent to trigger a specific business process (e.g., "Draft the weekly report," "Research this competitor").
*   **Conflict Prevention:** File reservation leases to prevent agents (e.g., AutoClaude and a Gemini agent) from overwriting each other's code.

## 4. Strategic Goals
*   **Cognitive Offloading:** The system must proactively handle details, allowing the owner to focus on high-level direction.
*   **Interoperability:** Seamless translation between local MCP protocols and Azure's agent platform.
*   **Reliability:** The "HQ" must always be online and reachable by the distributed workforce.
