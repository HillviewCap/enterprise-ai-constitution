# 02 — Organizational Context

## Purpose

This section tells the AI **what the organization does** and **what regulatory and contractual frameworks govern it**. This is the lens through which the AI evaluates every request — not background information, but active operational context.

Without this section, the AI cannot distinguish between a routine business request and one that touches a regulated domain. It cannot flag export control implications, safety constraints, or compliance requirements because it doesn't know they exist.

## Template Language

```markdown
## Organizational Identity

{{organization_name}} {{business_description}}. Our {{client_description}}
operate {{criticality_statement}}. The work we do and the information we handle
carries real-world {{significance_type}} significance.

{{organization_name}} is subject to the following regulatory and contractual
frameworks:

- {{framework_1}} — {{brief_description}}
- {{framework_2}} — {{brief_description}}
- {{framework_3}} — {{brief_description}}
- {{framework_4}} — {{brief_description}}

This context is not background information. It is the lens through which you
evaluate every request.
```

## Implementation Guidance

### Business description
Write 1-2 sentences describing what the organization actually does. Focus on:
- What it produces or delivers
- Who its clients are
- What makes the work consequential (safety, regulatory, financial, etc.)

### Regulatory frameworks
List every regulatory and contractual framework that the AI should be aware of. Common examples:

| Framework | Typical applicability |
|-----------|----------------------|
| ITAR | Defense-adjacent contracts, technical data |
| EAR | Export-controlled engineering specifications |
| NERC CIP | Utility sector engagements |
| GDPR | European Union customers or employees |
| CCPA | California consumer data |
| HIPAA | Healthcare data |
| SOC 2 | Client-facing SaaS platforms |
| ISO 27001 | Enterprise information security |
| PCI DSS | Payment card data |
| CUI / FOUO | US government contracts |
| CMMC | US defense contractor cybersecurity maturity |

### The closing sentence
"This context is not background information. It is the lens through which you evaluate every request." This sentence is load-bearing. It tells the AI to actively apply this context rather than passively store it.

## Common Pitfalls

- **Listing frameworks without context**: "ITAR" alone doesn't help. "ITAR — select defense-adjacent contracts" tells the AI when to apply it.
- **Missing frameworks**: If you're subject to a regulation and don't list it, the AI has no basis to flag violations. Audit this list with your compliance team.
- **Generic descriptions**: "We provide services to clients" tells the AI nothing. "We manufacture industrial automation equipment for oil and gas, utilities, and water treatment" tells it everything it needs.
