# Track Specification: Initialize Digital HQ Bridge & Unified Identity

## Goal
Transform the existing mcp_agent_mail project into the "Digital Headquarters" for the user's multi-agent workforce. This involves establishing a unified persistent environment ("One Family"), integrating Mem0 Enterprise for long-term memory, and defining the core "Co-Founder" and "QA" personas.

## Core Requirements

### 1. Unified Persistent Environment
*   **Objective:** Remove all legacy "Git Worktree" logic which isolated agents.
*   **Implementation:** 
    *   Delete scripts/docs related to ephemeral worktrees.
    *   Ensure all agents operate on the main codebase, synchronized via Agent Mail file leases.

### 2. Employee Registry & Persona Definition
*   **Objective:** distinct separation between "Operational Rules" and "Agent Personalities".
*   **Implementation:**
    *   **Refactor AGENTS.md:** Strip it down to be the "Constitution" (Safety rules, stack mandates, operational protocols).
    *   **Create conductor/EMPLOYEE_REGISTRY.md:** Define the specific agents:
        *   **Co-Founder (Ideation):** The "Boardroom" partner.
        *   **Natalia Reeves (QA):** The "Mama Bear" / "Bad Cop" ensuring quality.
        *   **Azure Foundry Agents:** Placeholders for cloud agents.

### 3. Enterprise Memory Infrastructure (Mem0)
*   **Objective:** Enable long-term memory and identity persistence.
*   **Implementation:**
    *   Add mem0ai dependency.
    *   Update gemini.mcp.json to include Mem0 configuration/API keys.
    *   Update mcp_agent_mail core to query Mem0 for agent context on startup/message receipt.

## Success Criteria
*   Legacy worktree code is removed.
*   AGENTS.md contains *only* operational rules.
*   EMPLOYEE_REGISTRY.md exists with at least the Co-Founder and QA personas defined.
*   Mem0 is installed and configured in the local environment.
