# Tools

## Constitution Builder

Interactive CLI tool that guides organizations through building AI constitution files with real-time token tracking.

### Quick Start

```bash
python tools/constitution-builder.py
```

### Usage

```
python constitution-builder.py [--tier {1,2,3}] [--budget TOKENS] [--output FILE]
```

| Flag | Description |
|------|-------------|
| `--tier 1` | Corporate constitution (organization-wide) |
| `--tier 2` | Team constitution (department-level addendum) |
| `--tier 3` | Practitioner constitution (individual context) |
| `--budget N` | Token budget — skip interactive selection |
| `--output FILE` | Output file path — skip filename prompt |

### Examples

```bash
# Interactive mode — prompts for everything
python tools/constitution-builder.py

# Build a corporate constitution with an 8,000 token budget
python tools/constitution-builder.py --tier 1 --budget 8000

# Build a team addendum, output to a specific file
python tools/constitution-builder.py --tier 2 --output constitutions/engineering-team.md

# Build a practitioner context with a tight budget
python tools/constitution-builder.py --tier 3 --budget 4000 --output contexts/jane-sre.md
```

### Tiers

The builder follows the [Context Onion](../docs/context-onion.md) layering model:

| Tier | Layer | Scope | Typical owner |
|------|-------|-------|---------------|
| **1** | Corporate | Organization-wide system instructions | CISO, AI Governance Council |
| **2** | Team | Department / team-level addendum | Team lead, manager |
| **3** | Practitioner | Individual operating context | The practitioner |

Each inner tier inherits and cannot relax the constraints of outer tiers.

### Token Tracking

Constitution files are injected as system prompts into AI chat and agent interfaces, which have finite context windows. The builder tracks token count throughout the process so you can stay within your deployment target's limits.

**Pre-set budgets:**

| Budget | Use case |
|--------|----------|
| 4,000 | Conservative — Copilot, smaller context windows |
| 8,000 | Standard — ChatGPT, Claude, Gemini, Cursor |
| 16,000 | Generous — dedicated system-prompt allocation |
| 32,000 | Large — custom deployments, RAG preambles |

**Token counting methods:**

- **tiktoken** (accurate): If `tiktoken` is installed (`pip install tiktoken`), the builder uses the `cl100k_base` encoding for precise counts matching OpenAI and Anthropic tokenizers.
- **Heuristic** (fallback): Without tiktoken, uses `max(chars/4, words*1.3)` — intentionally rounds up for conservative estimates.

### Dependencies

- **Python 3.10+** — uses standard library only
- **tiktoken** (optional) — `pip install tiktoken` for accurate token counting

### Output

The builder produces a ready-to-deploy markdown file matching the format in [`templates/`](../templates/). The output can be used directly as:

- A system prompt in chat interfaces (ChatGPT, Claude, etc.)
- A `CLAUDE.md` or similar project-level instruction file
- Input to MDM deployment tools (Intune, JAMF)
- A versioned governance document in git
