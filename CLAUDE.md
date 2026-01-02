# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

MCP Agent Mail is an HTTP-only FastMCP server that provides a mail-like coordination layer for coding agents. It enables agents to:
- Register memorable identities (adjective+noun names like "GreenCastle")
- Send/receive GitHub-Flavored Markdown messages with image attachments
- Declare advisory file reservations (leases) to prevent edit conflicts
- Search and thread conversations with FTS5 full-text search

**Architecture**: Dual persistence model with:
- Human-readable markdown in a per-project Git repo (auditable artifacts)
- SQLite with FTS5 for fast search, directory queries, and file reservations

## Common Commands

### Development Setup
```bash
# Create Python 3.14 venv and install dependencies
uv python install 3.14
uv venv -p 3.14
source .venv/bin/activate  # Or .venv\Scripts\activate on Windows
uv sync
```

### Running the Server
```bash
# Start HTTP server on port 8765
scripts/run_server_with_token.sh

# Or manually with uvicorn
uv run uvicorn mcp_agent_mail.http:build_http_app --factory --host 127.0.0.1 --port 8765
```

### Code Quality
```bash
# Lint and auto-fix (MANDATORY after code changes)
ruff check --fix --unsafe-fixes

# Type checking (MANDATORY after code changes)
uvx ty check
```

### Testing
```bash
# Run all tests
pytest

# Run single test file
pytest tests/test_server.py -v

# Run single test
pytest tests/test_server.py::test_function_name -v

# Skip slow/benchmark tests
pytest -m "not slow and not benchmark"
```

### CLI Commands
```bash
# Server configuration
uv run python -m mcp_agent_mail.cli config set-port 9000

# Guard installation (Git pre-commit hooks)
mcp-agent-mail guard install <project_key> . --prepush
mcp-agent-mail guard status .

# Project management
mcp-agent-mail projects mark-identity . --commit
mcp-agent-mail mail status .

# Product Bus operations
mcp-agent-mail products ensure MyProduct --name "My Product"
mcp-agent-mail products link MyProduct .
```

## Architecture

### Core Modules (`src/mcp_agent_mail/`)

| File | Purpose |
|------|---------|
| `app.py` | FastMCP server factory, all MCP tools organized by cluster (identity, messaging, file_reservations, macros, etc.) |
| `http.py` | FastAPI wrapper with CORS, JWT/RBAC auth, rate limiting, and Web UI routes (`/mail/*`) |
| `cli.py` | Typer CLI with subcommands: guard, file_reservations, acks, share, config, archive, mail, projects, products |
| `models.py` | SQLModel entities: Project, Agent, Message, MessageRecipient, FileReservation, AgentLink, Product |
| `db.py` | Async SQLAlchemy engine/session management with SQLite WAL mode and retry-on-lock decorator |
| `storage.py` | Git-backed archive operations, attachment processing, markdown bundle writing |
| `guard.py` | Pre-commit/pre-push hook logic for file reservation conflict detection |
| `config.py` | python-decouple Settings dataclasses (HttpSettings, DatabaseSettings, StorageSettings, etc.) |

### Tool Clusters (defined in `app.py`)

- **infrastructure**: `ensure_project`, `list_projects`, `delete_project`
- **identity**: `register_agent`, `update_agent`, `list_agents`, `generate_name`
- **messaging**: `send_message`, `fetch_inbox`, `acknowledge_message`, `reply_to_message`
- **file_reservations**: `file_reservation_paths`, `release_file_reservations`, `query_file_reservations`
- **workflow_macros**: `macro_start_session`, `macro_prepare_thread`, `macro_file_reservation_cycle`
- **build_slots**: `acquire_build_slot`, `renew_build_slot`, `release_build_slot`
- **product_bus**: `ensure_product`, `products_link`, `search_messages_product`

### Data Flow

```
Agents → HTTP POST /mcp → FastMCP tools → SQLite (queries) + Git repo (artifacts)
         ↓
Web UI → GET /mail/* → Jinja2 templates → HTML response
```

## Project Conventions

### Configuration
All settings loaded from `.env` using python-decouple pattern:
```python
from decouple import Config as DecoupleConfig, RepositoryEnv
decouple_config = DecoupleConfig(RepositoryEnv(".env"))
MY_SETTING = decouple_config("MY_SETTING", default="value")
```

### Database Operations
- Use `async with get_session() as session:` for all DB operations
- Use `selectinload`/`joinedload` for eager loading (no lazy loads in async)
- Apply `@retry_on_db_lock` decorator for SQLite lock resilience

### Console Output
Use the `rich` library for all console output (progress bars, tables, syntax highlighting).

### File Handling
- File reservation patterns use Git pathspec semantics
- Attachments are processed to WebP format and stored in Git
- Message bundles written as frontmatter YAML + markdown body

## Critical Rules from AGENTS.md

1. **Never delete files** without explicit user permission
2. **Never run destructive git commands** (`git reset --hard`, `git clean -fd`, `rm -rf`) without explicit approval
3. **Always use uv**, never pip. Target Python 3.14 only
4. **Always run lint and type checks** after code changes: `ruff check --fix --unsafe-fixes` and `uvx ty check`
5. **Never create versioned file copies** (no `file_v2.py`, `file_improved.py`, etc.) - edit in place
6. **Never run code modification scripts** - make changes manually or use parallel subagents
7. Consult `third_party_docs/PYTHON_FASTMCP_BEST_PRACTICES.md` for FastMCP patterns
8. Consult `third_party_docs/fastmcp_distilled_docs.md` for FastMCP library questions
