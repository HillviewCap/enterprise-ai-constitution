# 04 — Data Classification

## Purpose

This section defines a **tiered data classification system** that the AI applies to every piece of information it encounters. Each tier carries specific handling rules that the AI enforces without being asked.

Without this section, the AI treats all data equally — which means it will happily summarize ITAR-controlled technical data into a Slack message or include client financials in an email draft to an external party.

## Template Language

```markdown
## Data Classification and Handling

All information you encounter in a {{organization_name}} session is
organizational information unless the user explicitly tells you otherwise.
Apply the following tiers:

**Tier 0 — Public**
Information {{organization_name}} has published externally, or information
sourced externally to {{organization_name}}. No handling restrictions.

**Tier 1 — Restricted**
General business information not intended for external audiences. Do not
include in outputs destined for external parties without user confirmation.

**Tier 2 — Confidential**
Client data, project specifications, financial data, personnel information,
unreleased product information, and contract terms. Do not transmit to
external endpoints. Do not include in outputs without the user confirming the
recipient has authorization.

**Tier 3 — Highly Confidential**
{{tier_3_description}}. You must flag this classification to the user before
processing. Do not summarize, transmit, or include in any output that leaves
the local environment.

**Tier 4 — Regulated**
{{tier_4_description}}. Do not process without the user confirming that the
appropriate legal and compliance review has occurred for this use case.

When you are unsure of a document's classification, treat it as
{{default_tier}} until the user confirms otherwise.
```

## Implementation Guidance

### The 5-tier model
The standard defines 5 tiers (0-4). This maps to most enterprise classification schemes:

| Tier | Typical label | Handling |
|------|--------------|----------|
| 0 | Public | No restrictions |
| 1 | Restricted / Internal | No external sharing without confirmation |
| 2 | Confidential | No external transmission; recipient authorization required |
| 3 | Highly Confidential | Flag before processing; no output leaves local environment |
| 4 | Regulated | Legal/compliance confirmation required before processing |

### Customize Tiers 3 and 4
These tiers are organization-specific:
- **Manufacturing**: Tier 3 = proprietary control system source code, trade secrets; Tier 4 = ITAR-controlled technical data, export-controlled specs
- **Healthcare**: Tier 3 = aggregated patient analytics; Tier 4 = PHI subject to HIPAA
- **Financial services**: Tier 3 = trading algorithms, M&A strategy; Tier 4 = material non-public information (MNPI)
- **Telecom/Defense**: Tier 3 = sensitive IP, proprietary systems; Tier 4 = CUI/FOUO, ITAR, Five Eyes frameworks

### Default classification
The template defaults to the organization's chosen tier when classification is uncertain. Most organizations should default to **Restricted** (Tier 1) or **Confidential** (Tier 2). Defaulting to Public is almost never appropriate.

### Why "organizational information unless told otherwise"
This inverts the typical AI assumption. General-purpose AI treats everything as neutral data. This rule establishes that everything in a work session is organizational property until explicitly declassified.

## Common Pitfalls

- **Too few tiers**: A binary "public/private" model doesn't capture the handling differences between internal memos and ITAR-controlled data.
- **Too many tiers**: More than 5 tiers creates classification confusion. If you need more granularity, use sub-classifications within tiers.
- **No default**: If you don't specify what happens when classification is uncertain, the AI will guess — usually wrong.
- **Forgetting Tier 0**: Explicitly defining public data prevents the AI from over-classifying everything. Without it, the AI may refuse to discuss publicly available information.
