# Platform Compatibility Guide

> **Web version available:** This guide is available in an interactive format at [constitutionbuilder.ai/deploy.html](https://constitutionbuilder.ai/deploy.html) with expandable platform cards and testing status badges.

## Deploying Layer 1 (Corporate Constitution) Across Enterprise AI Tools

Layer 1 — the Corporate Identity layer — is the outermost ring of the [Context Onion](context-onion.md). It defines who the organization is, what it does, what regulations govern it, and what behavioral constraints apply to every AI interaction. It is read-only, non-negotiable, and deployed at the system level.

This guide maps Layer 1 deployment to every major enterprise AI platform. The goal: **regardless of which AI tool an employee uses, the organization's constitutional baseline is already in place before the first prompt.**

---

## Why Layer 1 First

Layer 1 provides the highest-impact governance improvement with the lowest implementation complexity:

- **Without Layer 1**, every AI session starts from zero. The AI has no organizational loyalty, no regulatory awareness, no data classification framework, and no basis for refusing inappropriate requests.
- **With Layer 1**, every AI session starts with identity, authority limits, data handling rules, and behavioral mandates already loaded — even if Layers 2 and 3 are never implemented.

Layer 1 alone transforms AI from "general-purpose tool an employee happens to use at work" to "organizational participant operating within defined boundaries."

---

## Platform Categories

Enterprise AI tools fall into four categories based on how they accept constitutional instructions:

| Category | Prompt Mechanism | Layer 1 Deployment Method |
|----------|-----------------|--------------------------|
| **File-based** | Instruction files committed to repos or deployed to endpoints | Deploy constitution as a managed file |
| **API-level** | System prompt parameter in API calls | Inject constitution server-side in application code |
| **Builder UI** | Agent/assistant configuration interfaces | Paste constitution into instructions field |
| **Policy-layer** | Guardrails, trust layers, governance gateways | Encode constitutional rules as platform policies |

Most organizations will use tools across multiple categories. The constitution content is the same — only the delivery mechanism changes.

---

## AI Coding Agents

These tools operate in developer environments. Layer 1 is deployed as managed instruction files on endpoints or in repositories.

### Claude Code (Anthropic)

| Aspect | Detail |
|--------|--------|
| **File** | `CLAUDE.md` (project root) for project-level; `~/.claude/CLAUDE.md` for user-level |
| **Enterprise lock mechanism** | `managed-settings.json` deployed at OS level |
| **Lock file locations** | Linux: `/etc/claude-code/managed-settings.json`; macOS: `/Library/Application Support/ClaudeCode/managed-settings.json` |
| **Drop-in directory** | `managed-settings.d/*.json` for modular policy deployment |
| **Deployment tools** | MDM (Intune, JAMF), configuration management (Ansible, Chef, Puppet), or manual |
| **Hierarchy** | Server-managed > OS-level managed-settings > user settings > project settings |
| **Layer 1 approach** | Deploy the corporate constitution as a managed `CLAUDE.md` at the enterprise level via MDM. Use `managed-settings.json` to enforce behavioral policies (tool permissions, allowed/denied commands). The constitution text goes in the CLAUDE.md; the enforcement rules go in managed-settings. |

**Implementation:**
1. Author the corporate constitution using the [corporate template](../templates/corporate-constitution.md)
2. Deploy to all managed endpoints via MDM or configuration management
3. Lock the file permissions so users cannot modify
4. Use `managed-settings.json` to enforce tool-level restrictions that complement the constitution

---

### GitHub Copilot

| Aspect | Detail |
|--------|--------|
| **File** | `.github/copilot-instructions.md` (repository root) |
| **Granular files** | `.github/instructions/**/*.instructions.md` (file-type-specific rules) |
| **Enterprise lock mechanism** | Enterprise-level policies in GitHub Enterprise Cloud admin console; cascade: Enterprise > Organization > Repository > Personal |
| **Cross-agent file** | Also reads `AGENTS.md` |
| **Layer 1 approach** | Set organization-level instructions in the GitHub Enterprise admin console. These apply to all repositories in the organization and cannot be overridden at the org or repo level when enforced at the enterprise tier. Supplement with `.github/copilot-instructions.md` in repos for Layer 2 team-level context. |

**Implementation:**
1. Adapt the corporate constitution for Copilot's instruction format (Markdown, natural language)
2. Deploy organization-level instructions via GitHub Enterprise Cloud admin settings
3. Enforce at enterprise level so organization admins cannot relax the policy
4. Use repository-level `copilot-instructions.md` for Layer 2 (team) context only

---

### Cursor

| Aspect | Detail |
|--------|--------|
| **File** | `.cursor/rules/*.md` (project-level rules with glob matching) |
| **Legacy file** | `.cursorrules` (deprecated) |
| **Enterprise lock mechanism** | Business/Enterprise dashboard distributes team-wide rules to all members via deeplinks |
| **Admin controls** | SSO (SAML), SCIM, RBAC, MDM policies; admins control model access, MCP servers, extensions |
| **Layer 1 approach** | Define the corporate constitution as team-wide rules in the Cursor Enterprise dashboard. These auto-distribute to all team members. Per-project `.cursor/rules/` files serve as Layer 2. |

**Implementation:**
1. Author constitutional rules in the Cursor Enterprise admin dashboard
2. Distribute to all seats via the centralized team rules feature
3. Use project-level `.cursor/rules/*.md` for team-specific context (Layer 2)

---

### Windsurf (Codeium)

| Aspect | Detail |
|--------|--------|
| **File** | `.windsurf/rules/*.md` (project-level) |
| **Legacy file** | `.windsurfrules` |
| **Enterprise lock mechanism** | System-level workflows deployed to OS-specific directories (read-only for users) |
| **Lock file locations** | macOS: `/Library/Application Support/Windsurf/workflows/*.md`; deployable via MDM |
| **Layer 1 approach** | Deploy the corporate constitution as a system-level workflow file via MDM. These are read-only — users cannot modify them. Project-level `.windsurf/rules/` files serve as Layer 2. |

**Implementation:**
1. Author the constitution as a Windsurf workflow Markdown file
2. Deploy to the OS-level system workflows directory via MDM or config management
3. Verify read-only permissions are enforced
4. Use `.windsurf/rules/*.md` in repos for Layer 2 context

---

### Amazon Q Developer

| Aspect | Detail |
|--------|--------|
| **File** | `.amazonq/rules/*.md` (project root) |
| **Enterprise lock mechanism** | Customizations managed centrally via AWS console + IAM; SCPs control feature availability org-wide |
| **Layer 1 approach** | Use AWS Organizations Service Control Policies (SCPs) to enforce baseline AI governance. Deploy customizations centrally via the AWS console to train code style. Supplement with `.amazonq/rules/*.md` in repos for project-level context. Note: project rules are not currently lockable at the enterprise level — rely on SCPs and IAM for enforcement. |

**Implementation:**
1. Define organizational AI policies as SCPs in AWS Organizations
2. Create centralized customizations in the AWS console for code-style governance
3. Deploy `.amazonq/rules/*.md` files in repos with corporate constitutional language
4. Use IAM Identity Center to control which users/groups access which customizations

---

### Google Gemini Code Assist

| Aspect | Detail |
|--------|--------|
| **File** | `.gemini/styleguide.md` (repository root) |
| **Commands** | `.gemini/commands.json` (reusable slash commands) |
| **Enterprise lock mechanism** | Group-level style guides in Google Cloud console (Enterprise tier); merged with repo-level guides |
| **Layer 1 approach** | Define the corporate constitution as a group-level style guide in the Google Cloud console. This applies across all repositories in the group. Repo-level `styleguide.md` files are merged with (not override) the group guide. |

**Implementation:**
1. Adapt constitutional language into a Gemini style guide format
2. Deploy as a group-level style guide via Google Cloud console (Enterprise tier required)
3. Use repo-level `.gemini/styleguide.md` for Layer 2 team context

---

### JetBrains AI Assistant

| Aspect | Detail |
|--------|--------|
| **File** | `.aiassistant/rules/*.md` (project root) |
| **Enterprise lock mechanism** | JetBrains IDE Services manages AI profiles centrally; "AI Enterprise" controls provider selection and model access |
| **Layer 1 approach** | Use JetBrains IDE Services to deploy centrally managed AI profiles with constitutional language. Supplement with `.aiassistant/rules/*.md` in repos for project-level context. |

**Implementation:**
1. Configure AI Enterprise profiles with constitutional policies via IDE Services
2. Deploy profiles to all managed IDE instances
3. Use project-level rules files for Layer 2 context

---

### Tabnine

| Aspect | Detail |
|--------|--------|
| **File** | `/.tabnine/guidelines/*.md` (per-project) or `~/.tabnine/guidelines/*.md` (global) |
| **Enterprise lock mechanism** | Admin UI > Agent Guidelines; admin guidelines **override** personal files — developers cannot bypass |
| **Layer 1 approach** | Deploy the corporate constitution as organization-wide guidelines in the Tabnine Admin UI. These take precedence over all user-level guidelines. |

**Implementation:**
1. Author the constitution as Tabnine admin guidelines in the Admin UI
2. Admin guidelines automatically override any user-level `guidelines.md` files
3. Use project-level `/.tabnine/guidelines/*.md` for Layer 2 context

---

### AGENTS.md (Cross-Tool Convention)

| Aspect | Detail |
|--------|--------|
| **File** | `AGENTS.md` (repository root; supports nested files in monorepos) |
| **Supported by** | GitHub Copilot, Cursor, Windsurf, OpenAI Codex, Zed, Aider, Semgrep, Warp, Factory |
| **Governed by** | Agentic AI Foundation (Linux Foundation) |
| **Layer 1 approach** | Deploy an `AGENTS.md` containing the corporate constitution at the root of every repository. This provides a tool-agnostic constitutional baseline that works across whichever coding agent an employee uses. Best used as a complement to tool-specific mechanisms, not a replacement — AGENTS.md has no enterprise lock mechanism since it lives in the repo. |

**Implementation:**
1. Create a standard `AGENTS.md` from the corporate constitution template
2. Commit to the root of every organizational repository
3. Protect via branch protection rules (require PR approval for changes to `AGENTS.md`)
4. Use as a supplement to tool-specific enterprise-managed mechanisms

---

## Enterprise Chat & Assistant Platforms

These platforms serve non-developer employees through conversational interfaces. Layer 1 is deployed through admin consoles, API configurations, or agent builder UIs.

### Microsoft Copilot (M365 + Copilot Studio)

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Declarative Agent instructions in Copilot Studio |
| **Enterprise lock mechanism** | Copilot Control System (CCS) + Agent 365 unified control plane; Entra ID governance |
| **Admin controls** | M365 Admin Center controls agent availability, creation permissions, lifecycle management |
| **Layer 1 approach** | Create a base Declarative Agent in Copilot Studio whose instructions contain the corporate constitution. Use CCS policies to enforce organizational boundaries. All custom agents built by teams (Layer 2) inherit the organizational policies enforced by CCS and Agent 365. |

**Implementation:**
1. Define organizational AI policies in the Copilot Control System
2. Create a base Declarative Agent with constitutional instructions in Copilot Studio
3. Use Agent 365 to enforce identity-based governance (Entra Agent ID)
4. Enable DLP, Defender, and audit logging as technical enforcement of constitutional rules
5. Teams create their own agents (Layer 2) within the boundaries set by organizational policy

---

### ChatGPT Enterprise (OpenAI)

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Custom GPTs with natural-language instructions; API developer messages |
| **Enterprise lock mechanism** | Domain allowlists, sharing scope restrictions, group permissions |
| **Admin controls** | Workspace admin dashboard; SOC 2 Type II; SSO/SCIM |
| **Layer 1 approach** | Create an organization-standard Custom GPT whose instructions contain the corporate constitution. Restrict the workspace so employees use the constitutional GPT by default. Use domain allowlists to control external integrations. For API usage, inject the constitution as the developer/system message server-side. |

**Implementation:**
1. Create a "Corporate Assistant" Custom GPT with full constitutional instructions
2. Set maximum sharing scope to workspace-only
3. Configure domain allowlists to restrict GPT actions to approved services
4. For API deployments: inject the constitution as the `developer` message in every API call
5. Use group permissions to control which teams access which GPTs (Layer 2)

**Limitation:** OpenAI does not currently support forcing all users to use a specific GPT. Users can create personal GPTs that lack constitutional instructions. Mitigate via policy + monitoring.

---

### Google Gemini for Workspace

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Admin Console toggles per service/OU; Vertex AI Agent Builder for custom agents |
| **Enterprise lock mechanism** | Google Admin Console, DLP policies, IAM |
| **Layer 1 approach** | Use Google Admin Console to control Gemini feature availability per organizational unit. For custom agents, deploy constitutional instructions via Vertex AI Agent Builder with IAM-scoped agent identities. Model Armor enforces prompt injection protection at the platform level. |

**Implementation:**
1. Configure Gemini access controls per OU in Google Admin Console
2. Enable DLP policies to prevent Gemini from accessing protected files
3. Build custom agents in Vertex AI Agent Builder with constitutional instructions
4. Use Model Armor and AI Protection for security enforcement
5. Team-specific agents (Layer 2) inherit organizational IAM policies

---

### Amazon Bedrock

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | System prompts set server-side via API; agent instructions in Bedrock console |
| **Enterprise lock mechanism** | IAM-enforced mandatory guardrails; AWS Organizations Bedrock Policies |
| **Layer 1 approach** | This is the strongest centralized enforcement model. Create Bedrock Guardrails encoding the constitutional rules (content filtering, denied topics, sensitive info filters). Enforce these guardrails via IAM policies so they apply to every model inference call across the organization. Deploy guardrails from a management account and enforce across member accounts via AWS Organizations. System prompts containing the constitutional identity are set server-side and never exposed to end users. |

**Implementation:**
1. Encode constitutional rules as Bedrock Guardrails (6 safeguard policy types)
2. Create IAM policies that mandate guardrails for all inference calls
3. Deploy guardrails from the AWS Organizations management account
4. Set constitutional system prompts server-side in all Bedrock applications
5. Use AgentCore Gateway + Cedar policies for deterministic tool-call enforcement

---

### Anthropic Claude Enterprise (claude.ai Teams/Enterprise)

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Projects with custom instructions on claude.ai; API system parameter |
| **Enterprise lock mechanism** | Managed policy settings; Compliance API for monitoring |
| **Layer 1 approach** | For claude.ai usage: create organization-standard Projects with constitutional instructions. For API usage: inject the constitution as the `system` parameter in every API call. For Claude Code: deploy via managed-settings and managed CLAUDE.md as described in the coding agents section above. Use the Compliance API for continuous monitoring. |

**Implementation:**
1. Create standard Projects on claude.ai with constitutional instructions
2. For API deployments: inject constitution as `system` parameter server-side
3. For Claude Code: deploy via OS-level managed-settings (see coding agents section)
4. Enable the Compliance API for automated policy monitoring
5. Use spend controls and usage analytics for governance oversight

---

### Salesforce Agentforce

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Agent instructions + Agent Script (deterministic guardrails) |
| **Enterprise lock mechanism** | Einstein Trust Layer; agents inherit Salesforce user permission model |
| **Layer 1 approach** | Encode the corporate constitution into Agent Script — this provides deterministic (not probabilistic) behavioral constraints. Agent instructions carry the organizational identity. The Einstein Trust Layer enforces PII masking, toxicity detection, and audit trails at the platform level. Agents automatically respect field-level security and sharing rules. |

**Implementation:**
1. Define constitutional behavioral rules as Agent Script constraints
2. Set constitutional identity and context in agent instructions
3. Configure Einstein Trust Layer for PII masking and zero-data-retention
4. Use Agentforce Testing Center to validate constitutional compliance across scenarios
5. Team-specific agents (Layer 2) inherit platform-level trust controls

---

### ServiceNow AI Agents

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Workflow-embedded agent configurations |
| **Enterprise lock mechanism** | AI Control Tower — cross-platform governance |
| **Layer 1 approach** | Configure agents within ServiceNow's workflow engine with constitutional instructions. Use AI Control Tower as the meta-governance layer — it can discover and manage agents from ServiceNow, Microsoft, and other platforms within a single console. This makes it a potential **single pane of glass for Layer 1 enforcement** across multiple AI platforms. |

**Implementation:**
1. Embed constitutional rules in ServiceNow agent configurations
2. Deploy AI Control Tower for cross-platform agent governance
3. Use CMDB integration for context-rich agent monitoring
4. Enforce consistent policies across all platforms ServiceNow discovers

---

### IBM watsonx

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Prompt templates in watsonx.ai Prompt Lab; versioned and shared |
| **Enterprise lock mechanism** | watsonx.governance — dedicated governance product |
| **Layer 1 approach** | Author the corporate constitution as a versioned prompt template in watsonx.ai. Use watsonx.governance for lifecycle management — translating regulatory requirements into enforceable policies. Agent monitoring (GA Q1 2026) tracks decisions and behaviors in real time against constitutional rules. |

**Implementation:**
1. Create the constitution as a versioned prompt template in Prompt Lab
2. Share the template across the organization with appropriate access controls
3. Deploy watsonx.governance for compliance management and drift detection
4. Enable agent monitoring for real-time behavioral oversight

---

### Cohere (North)

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | "Preamble" system prompt via API; safety mode settings |
| **Enterprise lock mechanism** | North platform with built-in security and compliance |
| **Layer 1 approach** | Set the corporate constitution as the preamble (system prompt) in all API calls. The preamble is controlled server-side — end users never see or modify it. Deploy on private cloud or on-premises for data-sovereign environments. |

**Implementation:**
1. Encode the constitution as the default preamble for all Cohere API calls
2. Set safety mode appropriately for the organizational risk profile
3. Deploy on private cloud/VPC/on-prem as data residency requires
4. Use audit logging and usage monitoring for compliance oversight

---

## Agent Orchestration Frameworks

These platforms are used by development teams building custom AI applications. Layer 1 is injected at the application layer or enforced by platform governance features.

### LangChain / LangSmith / LangGraph

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | LangChain Hub for versioned prompt templates; LangSmith Fleet centralized agent registry |
| **Layer 1 approach** | Publish the corporate constitution as a versioned prompt template in LangChain Hub. All agents built with LangChain pull from this template. LangSmith Fleet provides the centralized registry for discovering and governing all agents. |

### Amazon Bedrock AgentCore

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Cedar policy language — deterministic, external to agent code |
| **Layer 1 approach** | Encode constitutional rules as Cedar policies. The AgentCore Gateway enforces every tool call against these policies **before execution** — this is deterministic, not probabilistic. Framework-agnostic: works regardless of which agent framework or model is used. |

### Google Vertex AI Agent Builder

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | System instructions + IAM-scoped agent identities |
| **Layer 1 approach** | Set constitutional system instructions at the agent level. Use IAM to scope agent identities as first-class principals with least-privilege access. Model Armor and AI Protection provide security enforcement. |

### Microsoft Agent Framework (formerly AutoGen + Semantic Kernel)

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Platform-managed prompts with Azure integration |
| **Layer 1 approach** | Deploy constitutional rules via Azure governance controls. Prompt shields protect against injection. Microsoft Purview integration provides compliance framework. |

### Databricks / Mosaic AI

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Unity Catalog + Mosaic AI Gateway |
| **Layer 1 approach** | Use Unity Catalog for unified governance across all AI assets. Mosaic AI Gateway provides the centralized entry point with rate limiting, permissions, and credential management. Constitutional rules are enforced at the gateway level. |

### Snowflake Cortex

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Agent instructions via Cortex Agent APIs |
| **Layer 1 approach** | Configure agents with constitutional instructions. AI Governance Gateway enforces access control and budget limits. All processing stays within Snowflake's security perimeter — data sovereignty by design. |

### Palantir AIP

| Aspect | Detail |
|--------|--------|
| **Prompt mechanism** | Ontology-backed agent configs in Agent Studio |
| **Layer 1 approach** | The strongest ontological governance model. Constitutional rules are embedded in the platform's security model — all agent actions are governed by the same permissions framework as the broader Foundry/AIP platform. LLM access is scoped to task-minimum. Supports air-gapped and classified environments. |

---

## Cross-Platform Deployment Strategy

For organizations using multiple AI tools (which is most enterprises), deploy Layer 1 in tiers:

### Tier A — Immediate (highest impact, lowest effort)

These mechanisms lock the constitution at the platform level. Users cannot bypass them.

1. **Claude Code** — Deploy `managed-settings.json` + managed `CLAUDE.md` via MDM
2. **Amazon Bedrock** — IAM-enforced guardrails via AWS Organizations
3. **Tabnine** — Admin guidelines in the Admin UI (override user-level)
4. **GitHub Copilot** — Enterprise-level policies in admin console

### Tier B — Standard (requires admin console configuration)

These mechanisms provide strong centralized control through admin UIs.

5. **Microsoft Copilot** — Copilot Control System policies + Declarative Agent instructions
6. **ChatGPT Enterprise** — Corporate Custom GPT + workspace restrictions
7. **Cursor** — Enterprise dashboard team-wide rules
8. **Salesforce Agentforce** — Agent Script + Einstein Trust Layer
9. **Windsurf** — OS-level system workflows via MDM

### Tier C — Application-layer (requires development work)

These mechanisms require injecting the constitution in application code.

10. **Any API-based deployment** (Anthropic API, OpenAI API, Bedrock API, Cohere API) — Inject constitution as system/developer message server-side
11. **LangChain/LangSmith** — Publish as versioned Hub template
12. **Custom internal platforms** — Embed in prompt management layer

### Tier D — Supplementary (defense in depth)

These mechanisms complement but do not replace the above.

13. **AGENTS.md** — Commit to all repos; protect via branch rules
14. **Repository-level instruction files** (.github/copilot-instructions.md, .cursor/rules/, etc.) — For Layer 2 team context; not a substitute for enterprise-level enforcement
15. **ServiceNow AI Control Tower** — Cross-platform governance overlay

---

## Adapting the Constitution for Different Platforms

The [corporate constitution template](../templates/corporate-constitution.md) is written for AI assistants that process natural language instructions (which all platforms listed here do). When deploying across platforms, consider:

### Token/length constraints
Some platforms impose limits on system prompt length. The full corporate constitution template runs approximately 2,000-3,000 tokens when populated. If a platform constrains system prompt length:
- Prioritize sections 01 (Identity) and 02 (Organizational Context) — these establish the constitutional foundation
- Sections 04 (Data Classification) and 05 (Behavioral Mandates) are the next priority
- Sections 06-08 (Misuse Detection, Refusal Logic, Scope Limitations) can be condensed

### Platform-specific formatting
- **API-based platforms** (Bedrock, OpenAI, Anthropic, Cohere): Plain text or Markdown in the system message
- **File-based tools** (Claude Code, Cursor, Copilot, etc.): Markdown files
- **Builder UIs** (Copilot Studio, Agentforce): Paste into the instructions field; some support Markdown rendering
- **Policy engines** (Bedrock Guardrails, Cedar, CCS): Translate behavioral rules into platform-native policy syntax — the constitutional text informs the policy, but the policy is expressed in the platform's format

### What stays constant across all platforms
Regardless of delivery mechanism, every Layer 1 deployment must establish:
1. **Organizational identity** — Who the AI works for (Section 01)
2. **Regulatory context** — What frameworks govern the work (Section 02)
3. **Authority hierarchy** — This constitution overrides all other instructions (Section 01)
4. **Data classification** — How to handle information at different sensitivity levels (Section 04)
5. **Behavioral baseline** — Non-negotiable rules for every session (Section 05)

---

## Verification

After deploying Layer 1 to any platform, validate using the [test suite](../tests/). Key tests for Layer 1 verification:

- **Identity test**: Ask the AI "Who do you work for?" — it should name the organization, not describe itself as a general-purpose assistant
- **Authority test**: Attempt to override a constitutional rule via a user prompt — the AI should refuse
- **Regulatory awareness test**: Present a scenario involving a listed regulatory framework — the AI should flag the compliance implications
- **Data classification test**: Present information at various sensitivity levels — the AI should apply the correct handling rules

These tests should be run on every platform where Layer 1 is deployed to confirm the constitution is being respected by the underlying model.

---

*This guide covers platforms as of March 2026. The enterprise AI governance landscape is evolving rapidly. Review platform capabilities quarterly and update deployment mechanisms as platforms add new governance features.*
