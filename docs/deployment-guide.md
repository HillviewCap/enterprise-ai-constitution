# Deployment Guide

## How to Deploy an AI Constitution in Your Organization

This guide covers the practical mechanics of getting a constitution into production — from a markdown file on your screen to a system-level instruction governing AI behavior across your enterprise.

---

## Deployment Methods

### Method 1: System Prompt (API-level)

If your organization accesses AI models through APIs (Claude API, OpenAI API, Azure OpenAI, etc.), the constitution is deployed as the **system prompt** in every API call.

**Pros:** Centralized control, consistent enforcement, works with any client
**Cons:** Requires API infrastructure, constitution must fit within system prompt token limits

**Implementation:**
- Store the constitution in your configuration management system
- Include it as the `system` parameter in every API request
- Version control the document and deploy updates through your standard release process

### Method 2: CLAUDE.md / Configuration Files

For tools that support project-level or user-level configuration files (Claude Code, Cursor, etc.), the constitution is deployed as a configuration file.

**Hierarchy:**
1. `~/.claude/CLAUDE.md` — User-level (practitioner layer)
2. `project/CLAUDE.md` — Project-level (team layer)
3. System prompt — System-level (corporate layer, highest authority)

**Pros:** Works with local AI development tools, easy to iterate
**Cons:** User can potentially modify local copies (mitigated by integrity verification)

### Method 3: MDM / Configuration Management

For enterprise-wide deployment, use your existing device management platform to push the constitution to all managed endpoints.

**Platforms:**
- **Microsoft Intune** — Deploy as a configuration profile or script that places the file at a known path
- **JAMF** — Deploy via policy to macOS endpoints
- **Ansible/Chef/Puppet** — Deploy as a managed configuration file to servers and development machines
- **Group Policy** — Deploy to Windows endpoints via GPO file distribution

**Pros:** Centralized, auditable, tamper-resistant when combined with integrity verification
**Cons:** Requires MDM infrastructure, slower to update

### Method 4: Git Repository

Store the constitution in a dedicated repository. Teams clone or reference it.

**Pros:** Version controlled, collaborative, transparent change history
**Cons:** Requires user discipline to keep local copies current

---

## Token Budget Considerations

AI models have finite context windows. The constitution consumes tokens from that budget. Typical sizes:

| Constitution type | Approximate tokens |
|---|---|
| Corporate only (minimal) | 800-1,200 |
| Corporate only (full, with all sections) | 1,500-2,500 |
| Corporate + team | 2,000-3,500 |
| Corporate + team + practitioner | 2,500-4,500 |

**Guidelines:**
- Keep the corporate constitution as concise as possible. Every word consumes tokens that could be used for the user's actual task.
- Move detailed team-specific rules to the team layer rather than bloating the corporate constitution.
- The practitioner layer should be the smallest — preferences and role context, not policy.
- The integrity verification section (09) adds ~500-800 tokens. Consider whether the security benefit justifies the cost.

---

## Update and Versioning Strategy

### Versioning
- Use semantic versioning: `MAJOR.MINOR.PATCH`
- MAJOR: Structural changes (new sections, removed sections, authority hierarchy changes)
- MINOR: Content additions or modifications within existing sections
- PATCH: Typo fixes, clarifications that don't change meaning

### Change management
- Constitutional changes should go through formal review (CISO, AI Governance, or equivalent)
- Team-level changes should be approved by team leads
- Practitioner-level changes are self-service within team constraints
- Maintain a CHANGELOG for audit purposes

### Rollout
- Deploy to a pilot group first
- Monitor for false positives (legitimate work being blocked) and false negatives (misuse not being caught)
- Adjust before wide deployment

---

## Monitoring and Observability

### What to monitor
- **Refusal frequency** — High refusal rates may indicate overly restrictive rules or user confusion
- **Refusal categories** — Which sections trigger most often
- **Prompt injection attempts** — Detection rate and patterns
- **User workarounds** — Users rephrasing to avoid triggers (indicates friction points)

### Structured logging
If your AI platform supports session logging, consider the structured refusal tag approach:
```
<refusal category="data_exfiltration" section="misuse_detection" tier="2" />
```
This enables security teams to search and aggregate refusal patterns without reading full transcripts.

### Observability platforms
- **LangSmith / LangFuse** — AI-specific observability with tracing
- **Custom logging** — Capture system prompt + user prompt + response + any flags
- **SIEM integration** — Forward refusal events to your security monitoring platform

---

## Troubleshooting

### Users report the AI is "too restrictive"
- Review refusal logs for false positives
- Check if the data classification tiers are too aggressive for the team's actual work
- Consider adding a team-level constitution that clarifies approved workflows

### Users report the AI "doesn't know who it is"
- Verify the constitution is actually being loaded (check system prompt, file path, MDM deployment)
- Test with TC-01 (identity check) from the test suite
- Check for token truncation — if the constitution exceeds the system prompt limit, it may be silently truncated

### Prompt injection tests fail
- Verify the injection detection language in Section 06 is present and not truncated
- Test with simpler injection attempts first (TC-22 is the easiest to detect)
- Consider strengthening the injection detection language or adding examples
