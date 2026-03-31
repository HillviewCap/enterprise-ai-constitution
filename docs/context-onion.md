# The Context Onion

## A Layered Governance Model for Enterprise AI

The Context Onion is a design principle for structuring AI governance in layers — the same way regulated industries have structured human governance for decades.

Corporate policy sets the boundaries. Procedures interpret those boundaries for specific functions. Runbooks tell the practitioner exactly what to do in their operating environment. Each layer narrows the scope. Each layer builds on the one above it. Nobody hands a SCADA operator the corporate ethics charter and asks them to derive their daily operating constraints from first principles.

The Context Onion applies that same logic to AI.

---

## Three Layers

### Layer 1: Corporate Identity (Outermost)

Who the organization is, what it produces, who it serves, what regulations govern it, and what moral and ethical constraints it operates within. This is the constitution — deployed at the system level, read-only, non-negotiable. The AI doesn't discover this through conversation. It arrives knowing it.

**Governed by:** CISO, AI Governance Council, or equivalent authority
**Deployed via:** System-level instruction, MDM (Intune, JAMF), configuration management
**Changeability:** Constitutional amendments only — formal approval process

### Layer 2: Team / Function (Middle)

How corporate principles get interpreted for a specific group — a finance team, an engineering department, an OT operations crew. The risk profile changes. The permissible actions change. The standards that apply change.

**Governed by:** Team leads and managers — the people who write job descriptions and sign off on access requests
**Deployed via:** Team-level configuration files, project CLAUDE.md files
**Changeability:** Team lead approval

### Layer 3: Practitioner (Innermost)

The individual's operating environment, responsibilities, boundaries, and preferences. In organizations with mature identity management, this can be derived from existing role frameworks. In environments where that infrastructure doesn't exist yet, this layer can be bootstrapped through a structured initialization process — a series of well-crafted questions that capture what the operator does, what systems they touch, and what decisions they can make unilaterally.

**Governed by:** The practitioner, within bounds set by layers 1 and 2
**Deployed via:** User-level configuration, initialization conversation
**Changeability:** Updated when role, responsibilities, or system access changes

---

## How the Layers Interact

Each inner layer inherits from and is constrained by the layers outside it.

- A team constitution cannot relax a corporate rule. It can interpret it, narrow it, or add to it.
- A practitioner context cannot override team restrictions. It can specify preferences and working patterns within them.
- If any layer conflicts with an outer layer, the outer layer wins.

This is the same principle as defense-in-depth: each layer adds specificity without removing protections.

---

## Why This Matters

Without the Context Onion, every AI session starts from zero. The user must supply all organizational context every time. That's unreliable, unscalable, and places the governance burden on the person least equipped to carry it.

With the Context Onion, the AI arrives already knowing:
- Who it works for (corporate layer)
- What the team does and what rules apply (team layer)
- What this specific practitioner needs and is authorized to do (practitioner layer)

The user focuses on their task. The governance is already in place.

---

## Building the Onion

Not every organization arrives with all three layers ready to deploy.

**Starting point for most organizations:**
1. Deploy the corporate constitution first. This provides immediate, organization-wide baseline governance.
2. Add team layers as specific teams request them or as risk assessments identify the need.
3. Bootstrap practitioner layers through structured initialization for high-risk roles.

The corporate layer alone is a significant improvement over the status quo. Don't let the perfect be the enemy of the deployed.
