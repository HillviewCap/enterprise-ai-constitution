# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the **Enterprise AI Constitution Standard** — an open framework for governing AI behavior at the organizational level. It defines a 9-section standard for writing "AI constitutions" (system-level governance documents), along with templates, a CLI builder, a web app, and a test suite.

**Live site:** [constitutionbuilder.ai](https://constitutionbuilder.ai) (hosted on Cloudflare Pages)

## Architecture

The repo has two main dimensions: the **standard itself** (prose/markdown) and the **tooling** around it.

### The Standard (`standard/`)
Nine numbered sections (01-09) that must appear in order in a deployed constitution. Each section has a README with purpose, template language, implementation guidance, and pitfalls. Sections are addressed to the AI in second person ("You are...", "You must...").

### Three-Tier Governance Model ("Context Onion")
- **Tier 1 — Corporate** (`templates/corporate-constitution.md`): Organization-wide, read-only, non-negotiable
- **Tier 2 — Team** (`templates/team-constitution.md`): Function-specific addenda (engineering, legal, OT, etc.)
- **Tier 3 — Practitioner** (`templates/practitioner-constitution.md`): Individual operator context

Each tier narrows scope; inner tiers cannot override outer tiers.

### CLI Builder (`tools/constitution-builder.py`)
Interactive Python CLI that guides users through building constitutions with real-time token tracking. Uses `tiktoken` when available, otherwise a heuristic estimator.

```bash
python tools/constitution-builder.py                    # interactive mode
python tools/constitution-builder.py --tier 1           # corporate tier
python tools/constitution-builder.py --tier 2 --output my-team.md
python tools/constitution-builder.py --budget 4000      # token budget
```

No dependencies required (tiktoken is optional). Python 3 only.

### Web App (`site/`)
Static HTML/JS site deployed to Cloudflare Pages. Three pages: `index.html` (builder), `deploy.html` (deployment guide), `projects.html`. Uses DOMPurify for XSS protection. Security headers in `_headers`. Google Analytics via gtag.js.

### Tests (`tests/`)
24 manual test cases (`test-cases.md`) validated by deploying a constitution and submitting prompts. Not automated — results are compared against expected behavior by a human. Test cases cover identity, data classification, adversarial code review, misuse detection, prompt injection resistance, and refusal quality.

## Style Conventions

- Templates use `{{placeholder}}` syntax for fill-in fields
- Standard sections use second-person address to the AI
- Prefer specific, enforceable language over vague guidance (e.g., "Do not transmit Tier 2 data to personal accounts" not "be careful with sensitive data")
- Refusals must be non-accusatory, concise, and actionable
- Examples must be anonymized — no real company names or identifying details

## Deployment

The site deploys to Cloudflare Pages from the `site/` directory. To trigger a build, push to `main`.
