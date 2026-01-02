# Technology Stack

## 1. Core Platform & Backend
*   **Language:** Python 3.14 (Leveraging latest async/await features).
*   **API Framework:** **FastAPI**. Chosen for native async support, high performance, and ease of creating SSE/HTTP streamable endpoints required by Azure DirectLink.
*   **Orchestration:** **AutoClaude (Refactored)**. Evolving the existing codebase into a unified "Digital HQ" service, stripping out legacy git worktree logic in favor of a persistent environment.

## 2. Agent Communication & Coordination
*   **Protocol:** **MCP (Model Context Protocol)**. The universal language for all tools and agent interactions.
*   **Message Bus:** **MCP Agent Mail**.
    *   **Pattern:** "The Library Model" (File Reservation Leases). Agents must "check out" files before editing to prevent conflicts, ensuring serialized access to shared resources.
    *   **Transport:** HTTP-only FastMCP server backed by SQLite and Git.
*   **Bridge Protocol:** **A2A (Agent-to-Agent)** (Provisional). To be investigated for standardized inter-agent signaling if native MCP needs extension.

## 3. Memory & Context
*   **Primary Memory:** **Mem0 Cloud Enterprise**. The "Company Brain" storing persistent employee records, career histories, and shared business context.
*   **Context Management:** **Google ADK "Tiered Context" Architecture**. Implementing Working Context, Session, Memory, and Artifact Handles to manage token usage efficiency.

## 4. Infrastructure & Hosting
*   **Local Environment (The Office):**
    *   **OS:** Windows 10/11 (WSL2 optional).
    *   **Role:** The physical "source of truth" for files and code execution.
    *   **Local Tools:** Gemini CLI, Claude Code, Desktop Commander.
    *   **Configuration:** gemini.mcp.json serves as the template for local MCP connectivity.
*   **Cloud Endpoint (The Gateway):**
    *   **Provider:** Railway, Google Cloud Run, or similar.
    *   **Role:** Hosts the public-facing API for MCP Agent Mail and the "Digital HQ" bridge.
    *   **Connectivity:** **Azure DirectLink**. Exposes the local MCP servers (via secure tunnel like ngrok/Cloudflare) or hosted replicas to the Azure Foundry agents.

## 5. Microsoft Azure Foundry Integration
*   **Agent Platform:** **Microsoft Foundry**. Hosts the specialized cloud agents (e.g., "Agent Guardian").
*   **Native Tools:** Usage of Azure's "Code Interpreter" and "File Search" for internal agent reasoning.
*   **Custom Tools Integration:**
    *   **Remote MCP Endpoints:** Connecting Azure agents to the Digital HQ via standard HTTP/SSE MCP endpoints.
    *   **Desktop Commander Bridge:** Giving Azure agents controlled, remote access to local files via a secured tunnel to the Desktop Commander MCP.

## 6. Development Standards (The Constitution)
*   **Operational Rules:** Defined in AGENTS.md.
    *   **Safety:** "Break Glass" protocols for destructive actions.
    *   **Stack:** Strict adherence to Python 3.14, uv (no pip), and pyproject.toml.
    *   **Libraries:** FastMCP, SQLModel (Async), python-decouple.
*   **Version Control:** Git (GitHub).
*   **CI/CD:** GitHub Actions (triggered via GitHub MCP).
