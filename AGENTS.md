---
framework_version: 1.0.0
---

# Agent Guidelines: AI Job Search

## Local RU workflow (project-specific override)

For this adaptation, start by reading `AI_JOB_SEARCH_RU_SKILL_FINAL.md`, then the canonical upstream references it names. The first deliverable is a short Russian cover letter for a user-provided posting, researched against the company and grounded in confirmed candidate facts. Do not require search, ranking, a new CV, LaTeX, or PDF compilation for this text-only path. Do not execute the full upstream `/apply` unless the user requests that package.

Use the original Python tools through `.runtime/python/cpython-3.12.14-windows-x86_64-none/python.exe` (Windows Store `python` aliases do not work here). Use `tools/posting_guard.py` for incoming postings and `tools/fetch_page.py` / `tools/robots_check.py` for research fallbacks. Use the session's web-search tools for company discovery; these Python utilities do not generate letters or call an LLM themselves.

Keep the user's CodeGraph and personal development skill instructions. This is a new import, not yet CodeGraph-indexed; do not initialize the index without the user's permission. Do not treat upstream profile placeholders as candidate facts. Never send applications automatically.

This workspace is structured to manage job search activities, scraper tools, CVs, cover letters, and interview preparation.

## Thin-Pointer Design (Single Source of Truth)

To prevent duplication and configuration drift across different AI agent frameworks (Claude Code, Google Antigravity, Codex, Cursor, Gemini CLI, etc.), this workspace uses a unified thin-pointer design. All agent runtimes should load the canonical specifications and candidate profiles from the files and directories below:

1. **Personal Candidate Profile:**
   - The candidate profile, contact details, education, and target preferences are defined in [CLAUDE.md](CLAUDE.md) and the individual profile methodology files under [.claude/skills/job-application-assistant/](.claude/skills/job-application-assistant/) (specifically `01-*.md` etc.).
2. **Canonical Workflow Specifications:**
   - The step-by-step instructions and triggers for tasks (setup, scrape, rank, apply, upskill, interview) are defined in the [.claude/](.claude/) directory (specifically under `.claude/skills/` and `.claude/commands/`).
   - Do not duplicate these rules or specifications. Treat `.claude/` files as the single source of truth.
3. **Portal Search Skills:**
   - Job-portal search CLIs live under [.agents/skills/](.agents/skills/) in the portable Agent Skills format (with a `SKILL.md` per portal). Codex and Antigravity discover these automatically; the `/scrape` workflow in [.claude/skills/job-scraper/](.claude/skills/job-scraper/) orchestrates them.
