# Test Suite

## Purpose

This test suite validates that a deployed AI constitution produces the expected behavioral outcomes. It covers identity, data classification, adversarial code review, irreversible action handling, external communications, misuse detection, prompt injection resistance, and refusal quality.

## How to Run

1. Deploy your constitution as the system-level instruction in your AI tool (Claude Workbench, API system prompt, CLAUDE.md, etc.)
2. Submit each test prompt exactly as written
3. Compare the AI's response against the expected behavior
4. Log pass/fail and any notable deviations in the test log

## Test Coverage

| Category | Test Cases | What It Validates |
|----------|-----------|-------------------|
| Identity & Role | TC-01 to TC-03 | AI knows who it is, maintains constitutional hierarchy |
| Data Classification | TC-04 to TC-07 | Correct tier identification and handling across all tiers |
| Adversarial Code Review | TC-08 to TC-10 | Proactive security detection without false positives |
| Irreversible Actions | TC-11 to TC-12 | Confirmation required before destructive operations |
| External Communications | TC-13 to TC-14 | Human review flagged for outbound content |
| Misuse Detection | TC-15 to TC-19 | Personal use, exfiltration, bypass, credential access |
| Prompt Injection | TC-20 to TC-22 | Resistance to document, code, and social engineering injection |
| Refusal Quality | TC-23 to TC-24 | Refusals are clear, non-punitive, and actionable |

## Customization

Before running the tests, replace organization-specific references:
- "Meridian Industrial" with your organization name
- "IT Security team" with your exception authority
- Regulatory frameworks with your applicable frameworks
- Data classification examples with your tier definitions

## Important Notes

- All tests are **single-turn**. Multi-turn adversarial testing (escalation chains, social engineering sequences) should be developed separately.
- A passing test suite does not guarantee the constitution will hold under sustained adversarial pressure. It validates baseline behavior.
- False positives on TC-10 (secure code flagged as insecure) are a signal to tune the adversarial code review language.

## Full Test Cases

See [test-cases.md](test-cases.md) for all 24 test case definitions with prompts, expected behavior, and failure indicators.
