# The Standard

This directory contains the 9 sections of the Enterprise AI Constitution Standard. Each section addresses a distinct governance concern and includes:

- **Purpose** — What this section accomplishes
- **Template language** — Ready-to-adapt text written in second person, addressed to the AI
- **Implementation guidance** — Notes on how to customize for your organization
- **Common pitfalls** — Mistakes to avoid

## Section Order

Sections are numbered and should appear in this order in a deployed constitution. The ordering is intentional — identity and context must be established before behavioral rules reference them.

| # | Section | Required? |
|---|---------|-----------|
| 01 | Identity | Yes |
| 02 | Organizational Context | Yes |
| 03 | Authority Limits | Yes |
| 04 | Data Classification | Yes |
| 05 | Behavioral Mandates | Yes |
| 06 | Misuse Detection | Yes |
| 07 | Refusal Logic | Yes |
| 08 | Scope Limitations | Yes |
| 09 | Integrity Verification | Optional |

## How to Use

1. Read through each section's README to understand its purpose
2. Use the [corporate template](../templates/corporate-constitution.md) as your starting point
3. Customize the template with your organization's specifics
4. Deploy as a system-level instruction to your AI tooling
5. Validate using the [test suite](../tests/)

## Design Principles

- **Constitutional authority**: The constitution overrides all team-level and project-level instructions. This is by design.
- **Specificity over generality**: "Do not transmit Tier 2 data to personal accounts" is enforceable. "Be careful with sensitive data" is not.
- **Non-accusatory tone**: Every refusal and flag must be professional and non-punitive. Adoption depends on users trusting the system.
- **Brevity in enforcement**: When the AI refuses or flags, it should be concise — state the rule, state the alternative, move on. Over-explanation creates friction.
