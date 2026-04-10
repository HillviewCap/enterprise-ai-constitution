# Personal AI Constitution — Design Specification
**Project:** constitutionbuilder.ai  
**Repo:** https://github.com/HillviewCap/enterprise-ai-constitution  
**Date:** 2026-04-09  
**Version:** 2.0  
**Status:** Draft — research complete, ready for review

---

## The Problem

Every major AI platform now offers memory — Claude, ChatGPT, Gemini, Copilot, Meta AI. Over weeks and months these systems build a picture of who you are. But this approach has three fundamental problems:

1. **Cold start.** Every new tool, every new account, every cleared history starts from zero. You re-explain yourself over and over.
2. **Platform lock-in.** Your Claude memories don't travel to ChatGPT. Your ChatGPT Custom Instructions don't transfer to Gemini. Your AI context is scattered across walled gardens.
3. **Passive accumulation.** Memories are inferred from conversations — the AI decides what matters about you. You never sit down and deliberately articulate: *who am I, what do I believe, how do I work, and what do I need from AI?*

The enterprise version of this problem is solved by constitutional governance documents (the existing Constitution Builder). The personal version remains unsolved.

---

## The Solution

A guided builder that helps anyone — developer, consultant, student, creative, executive — articulate their **Personal AI Constitution**: a structured document capturing who they are, what they believe, how they work, and what they need from AI.

The builder produces **platform-specific exports** optimized for each major AI tool's memory ingestion pathway. One session, every platform.

**Core question this tool answers:**  
*"If you could brief every AI you use on who you are before your first conversation, what would you say?"*

---

## Inspiration and Prior Art

### Daniel Miessler's Personal AI Infrastructure (PAI)
GitHub: `danielmiessler/Personal_AI_Infrastructure` (11K+ stars)

PAI introduced the concept of structured self-knowledge for AI through its **TELOS system** — a set of markdown files that capture mission, beliefs, goals, mental models, strategies, narratives, lessons learned, challenges, ideas, and projects. Combined with identity files (ABOUTME.md, WRITINGSTYLE.md, OPINIONS.md), TELOS gives AI comprehensive context about the user.

**What PAI does well:**
- Comprehensive taxonomy of personal context (TELOS)
- Philosophy that AI should magnify human capabilities, not replace them
- Separation of user-owned data from system infrastructure
- The concept that structured self-knowledge improves every AI interaction

**Where this project differs:**
- **Accessibility.** PAI requires Claude Code, Bun runtime, TypeScript, and developer-level comfort with `~/.claude/` directory structures. This tool is a web-based guided experience for anyone.
- **Portability.** PAI produces Claude Code-specific files. This tool produces exports for every major platform.
- **Simplicity.** PAI is full infrastructure (21 hooks, 63 skills, 14 agents). This tool produces a document — your personal AI context — that you take wherever you go.
- **On-ramp.** PAI is the destination for power users. This tool is the on-ramp that helps you articulate what PAI assumes you already know about yourself.

### Enterprise AI Constitution Builder (existing)
The existing Constitution Builder at constitutionbuilder.ai answers: *"Who is this AI in my organization?"* The Personal Constitution answers the complementary question: *"Who am I to this AI?"*

The two products share a philosophical foundation — that AI performs better when given explicit context about identity, values, and boundaries — but serve different audiences and produce different outputs.

---

## Platform Landscape: Memory Ingestion Pathways (April 2026)

Research into every major AI platform's memory system reveals the delivery mechanisms we need to target:

### Claude (Anthropic)
| Pathway | Format | Limit | How to deliver |
|---------|--------|-------|----------------|
| **Claude.ai memory import** | Structured natural-language text block | No hard limit (processes over ~24hrs) | Settings > Capabilities > Import |
| **Claude Code CLAUDE.md** | Markdown file | ~200 lines recommended | Save to `~/.claude/CLAUDE.md` |
| **API Memory Tool** | Markdown files in virtual `/memory` dir | Developer-managed | Beta API (`memory_20250818`) |

Claude.ai's memory import tool (launched March 2026) is the most direct bulk ingestion path available on any platform. It accepts a block of text, extracts facts, and stores them as discrete memories.

### OpenAI (ChatGPT)
| Pathway | Format | Limit | How to deliver |
|---------|--------|-------|----------------|
| **Custom Instructions** | Two free-text fields | 1,500 characters each (3,000 total) | Settings > Personalization |
| **Custom GPT Knowledge Files** | PDF, TXT, MD, JSON, CSV, DOCX | 20 files, 512 MB total | GPT Builder > Knowledge |
| **Conversational memory** | Natural language ("remember this") | ~200 discrete memories | Paste block + "remember all of this" |
| **Assistants API vector stores** | Uploaded files | Developer-managed | API only |

ChatGPT has no bulk memory import. The most reliable path is Custom Instructions (small but persistent) + a Custom GPT Knowledge File (large, searchable). The conversational "remember all this" approach is unreliable — ChatGPT often captures only a subset.

### Google (Gemini)
| Pathway | Format | Limit | How to deliver |
|---------|--------|-------|----------------|
| **Gems system instructions** | Free text | Large (thousands of tokens) | Create Gem > Instructions |
| **Conversational memory** | Natural language | Platform-managed | Say "remember this" |

No bulk import. Gems are the best path — create a personal context Gem with the full constitution as its instructions.

### Microsoft (Copilot)
| Pathway | Format | Limit | How to deliver |
|---------|--------|-------|----------------|
| **Custom Instructions** | Free text | Several hundred words | Settings > Custom Instructions |
| **Copilot Studio agents** | JSON manifest + documents | Enterprise-managed | Copilot Studio |

### Meta AI
| Pathway | Format | Limit | How to deliver |
|---------|--------|-------|----------------|
| **Conversational memory** | Natural language | Platform-managed | Say "remember this" |

No bulk import, no custom instructions. Only conversational memory injection.

### PAI (Daniel Miessler's infrastructure)
| Pathway | Format | Limit | How to deliver |
|---------|--------|-------|----------------|
| **TELOS files** | Markdown (.md) | No limit | Save to `~/.claude/PAI/USER/TELOS/` |
| **Identity files** | Markdown (.md) | No limit | Save to `~/.claude/PAI/USER/` |

### Universal / API developers
| Pathway | Format | Limit | How to deliver |
|---------|--------|-------|----------------|
| **System prompt injection** | Plain text | Model context window | Prepend to API calls |

---

## Personal Context Taxonomy

Inspired by PAI's TELOS but simplified for accessibility. The builder walks through **7 categories** of self-knowledge. Each category maps to a section in the output document.

### 1. Identity — Who You Are
*The foundation. Everything else references back to this.*

- Name and how you prefer to be addressed
- Role(s) — professional title, side projects, personal identity
- One-paragraph bio (the "elevator pitch" version of you)
- Domain expertise (what you know deeply)
- What you're currently learning or exploring

**Why this matters to AI:** Sets the baseline for every response. An AI that knows you're a 20-year cybersecurity veteran responds differently than one that thinks you're a beginner. An AI that knows you're also a woodworker can draw cross-domain analogies.

### 2. Beliefs & Values — What You Hold True
*Your worldview. The lens through which you evaluate AI suggestions.*

- Core beliefs about your field (e.g., "Security is a process, not a product")
- Values that guide your decisions (e.g., "Open source over proprietary when quality is comparable")
- Principles you won't compromise on (e.g., "Never sacrifice safety for speed in critical infrastructure")
- Philosophical positions relevant to your work (e.g., "Defense in depth over perimeter security")

**Why this matters to AI:** An AI that knows your values can align suggestions with your worldview rather than defaulting to generic "best practices." It can flag when a suggestion might conflict with something you care about.

### 3. Goals & Mission — Where You're Headed
*Direction. What you're trying to accomplish and why.*

- Professional mission (your "why")
- Current goals — short-term (this month), medium-term (this quarter/year), long-term (career arc)
- Active projects and their status
- What success looks like for you right now

**Why this matters to AI:** An AI that knows your goals can proactively connect today's task to your larger objectives. It can flag opportunities you might miss and deprioritize work that doesn't serve your direction.

### 4. Working Style — How You Operate
*The practical details of how you get things done.*

- Communication preferences (concise vs. detailed, formal vs. casual)
- Decision-making style (data-driven, intuitive, consensus, etc.)
- Tools, platforms, and tech stack
- OS, editor, shell, languages
- Work patterns (deep focus blocks, pair programming, async-first, etc.)
- What drains your energy vs. what energizes you

**Why this matters to AI:** An AI that knows you prefer concise answers won't write walls of text. One that knows you use Fedora + Neovim + Python won't suggest macOS-specific tools or JavaScript solutions.

### 5. Knowledge & Expertise — What You Bring
*Your intellectual inventory. What the AI can lean on vs. what it should explain.*

- Areas of deep expertise (the AI can be terse here)
- Areas where you're competent but not expert (the AI should be precise)
- Areas where you're learning (the AI should explain thoroughly)
- Frameworks, methodologies, or mental models you use regularly
- Books, thinkers, or resources that shaped your thinking

**Why this matters to AI:** Calibrates explanation depth. An AI that knows you've read Kahneman can reference System 1/System 2 thinking without explaining it. One that knows you're new to React should explain component lifecycles, not assume you know them.

### 6. Boundaries & Preferences — What You Need From AI
*The rules of engagement. How AI should behave in your sessions.*

- What AI should always do (e.g., "Flag security concerns proactively")
- What AI should never do (e.g., "Don't add features I didn't ask for")
- How AI should handle uncertainty (e.g., "Say you don't know rather than guessing")
- How AI should handle disagreement (e.g., "Push back if my approach has obvious problems")
- Confirmation requirements (e.g., "Always confirm before destructive actions")
- Output format preferences (e.g., "Markdown tables over prose for comparisons")

**Why this matters to AI:** These are the behavioral mandates — the constitutional layer. They prevent the AI from learning bad habits and ensure consistent behavior across every session.

### 7. Context & Environment — What Surrounds You
*The ecosystem you operate in. Org, team, tools, constraints.*

- Organization / company / client context (if applicable)
- Team structure and your role in it
- Constraints (regulatory, technical, budget, timeline)
- External tools and services in your workflow
- Recurring tasks or responsibilities

**Why this matters to AI:** Grounds responses in your reality. An AI that knows you work in a regulated industry won't suggest "move fast and break things." One that knows your team uses Jira can format outputs accordingly.

---

## Output Format Specifications

The builder produces one canonical document and multiple platform-specific exports. The user fills out the builder once; the tool handles format conversion.

### Canonical Format: Personal AI Constitution (Markdown)

The full, uncompressed document. Human-readable, version-controllable, platform-agnostic.

```markdown
# Personal AI Constitution
<!-- Owner: {{name}} | Version: 1.0 | Date: {{date}} -->
<!-- Generated at constitutionbuilder.ai/personal -->

## About This Document
This is my Personal AI Constitution — a structured briefing document for any 
AI system I work with. It captures who I am, what I believe, how I work, and 
what I need from AI. Use it to ground your responses in my actual context 
rather than generic defaults.

If an organizational or team-level AI constitution is also active in this 
environment, that document takes precedence over this one.

---

## Who I Am

{{identity_prose}}

---

## What I Believe

{{beliefs_prose}}

---

## Where I'm Headed

### Mission
{{mission_statement}}

### Current Goals
{{goals_list}}

### Active Projects
| Project | Description | Status |
|---------|-------------|--------|
{{projects_table}}

---

## How I Work

{{working_style_prose}}

### Technical Environment
- **OS:** {{os}}
- **Editor:** {{editor}}
- **Shell:** {{shell}}
- **Languages:** {{languages}}
- **Stack:** {{stack}}

---

## What I Know

### Deep Expertise (be terse, I know this)
{{expertise_deep}}

### Competent (be precise)
{{expertise_competent}}

### Learning (explain thoroughly)
{{expertise_learning}}

### Frameworks & Mental Models I Use
{{mental_models}}

---

## Rules of Engagement

**These are behavioral mandates, not suggestions.**

### Always
{{always_rules}}

### Never
{{never_rules}}

### When Uncertain
{{uncertainty_rules}}

---

## My Context

{{context_prose}}

---

*Generated with [Constitution Builder](https://constitutionbuilder.ai/personal) | Version 1.0 | {{date}}*
*This document is meant to be updated as you grow. Review quarterly.*
```

Estimated size: 2,000–6,000 tokens depending on detail level.

### Export: Claude.ai Memory Import

Restructured as a flat list of natural-language factual statements — the format Claude.ai's memory import tool expects. Each statement is a discrete, self-contained fact.

```text
## About Me
My name is {{name}}. I go by {{preferred_name}}.
I work as a {{role}}.
{{bio_sentence_1}}
{{bio_sentence_2}}

## My Expertise
I have deep expertise in {{expertise_1}}, {{expertise_2}}, and {{expertise_3}}.
I am currently learning {{learning_1}} and {{learning_2}}.
I think in terms of {{mental_model_1}} and {{mental_model_2}}.

## My Beliefs and Values
I believe that {{belief_1}}.
I believe that {{belief_2}}.
I value {{value_1}} over {{value_2}}.

## My Goals
My professional mission is {{mission}}.
My current short-term goal is {{goal_short}}.
My current long-term goal is {{goal_long}}.

## How I Prefer to Work with AI
I prefer {{communication_style}} responses.
I use {{os}}, {{editor}}, and {{shell}} as my primary tools.
Always {{always_rule_1}}.
Always {{always_rule_2}}.
Never {{never_rule_1}}.
Never {{never_rule_2}}.
When you are uncertain, {{uncertainty_rule}}.
```

Each line should be parseable as a standalone memory entry. No section depends on another section for context.

### Export: Claude Code CLAUDE.md

The canonical Markdown format, saved as `CLAUDE.md`. Identical to the canonical format but with a header comment indicating deployment scope:

```markdown
<!-- Deployment: ~/.claude/CLAUDE.md (global) -->
<!-- To scope to a single project, save as ./CLAUDE.md in the project root -->
```

### Export: ChatGPT Custom Instructions

Two fields, each under 1,500 characters. This requires aggressive compression.

**Field 1 — "What would you like ChatGPT to know about you?"**
```text
I'm {{name}}, a {{role}}. {{compressed_bio}}

Expertise: {{top_3_deep_areas}}. Learning: {{top_2_learning_areas}}.

I believe: {{top_3_beliefs_compressed}}.

Current focus: {{current_goal_compressed}}.

Tools: {{os}}, {{editor}}, {{languages}}.
```

**Field 2 — "How would you like ChatGPT to respond?"**
```text
{{communication_preferences_compressed}}

Always: {{top_3_always_rules}}
Never: {{top_3_never_rules}}
When uncertain: {{uncertainty_rule_compressed}}

I know {{deep_expertise}} well — be terse there.
I'm learning {{learning_areas}} — explain those thoroughly.
```

The builder must show a live character count for each field and warn when approaching 1,500.

### Export: ChatGPT Custom GPT Knowledge File

The full canonical document, exported as a `.md` file for upload to a Custom GPT's Knowledge section. No compression needed — the 512 MB limit is generous.

### Export: Gemini Gem Instructions

The full canonical document reformatted slightly for Gem system instructions — remove the HTML comments and the "About This Document" preamble, and add an instruction prefix:

```text
You are a personal AI assistant. The following document describes who 
you are working with. Use it to ground all responses in this person's 
actual context, expertise, and preferences.

---

{{canonical_document_body}}
```

### Export: PAI TELOS Files

For users running Daniel Miessler's PAI, export individual files matching the TELOS structure:

```
MISSION.md    ← from Goals & Mission section
GOALS.md      ← from Goals & Mission section  
BELIEFS.md    ← from Beliefs & Values section
PROJECTS.md   ← from Goals & Mission > Active Projects
ABOUTME.md    ← from Identity section
```

Each file formatted as simple Markdown with no frontmatter (matching PAI's expected format).

### Export: Raw System Prompt

For developers building API integrations. The canonical document wrapped in a system prompt frame:

```text
<user_context>
{{canonical_document_body}}
</user_context>

Use the above context to personalize all responses for this user.
When the user's stated preferences conflict with generic best practices,
defer to the user's preferences unless doing so would cause harm.
```

---

## Product Tiers

The builder ships as a tiered product — free form-based wizard at the base, paid voice conversation as the premium experience.

### Tier 1 — Free: Form-Based Wizard
- **Experience:** 7-step guided form (same as described below in Builder Experience)
- **Cost to user:** $0
- **Cost to operate:** $0 (static site, no API calls, no server)
- **Infrastructure:** Cloudflare Pages (existing), pure client-side HTML/JS
- **Value prop:** "Build your Personal AI Constitution in 10 minutes. Export to every major platform."

### Tier 2 — Voice: Guided Conversation (Gemini Flash Live)
- **Experience:** Real-time voice conversation with an AI interviewer that asks questions, follows up, and builds the constitution through natural dialogue
- **Cost to user:** $3-5/session (one-time, no subscription)
- **Cost to operate:** ~$0.35/session (Gemini 3.1 Flash Live API via Vertex AI)
- **Infrastructure:** Vertex AI (user's existing Google Cloud environment), WebSocket-based Live API, browser microphone access
- **Value prop:** "Talk through your constitution instead of typing. Like being interviewed by a thoughtful colleague."

**Why Gemini Flash Live:**
- $0.023/min combined audio I/O — by far the cheapest native voice API
- Bidirectional WebSocket with native turn detection and interruption handling
- Free tier available on ai.google.dev for development/testing
- Vertex AI deployment leverages existing Google Cloud infrastructure
- Multi-turn session context accumulation — the AI remembers the full conversation

**Technical flow:**
1. User clicks "Start Voice Session" → browser requests microphone permission
2. WebSocket connection opens to Gemini Live API via Vertex AI endpoint
3. System prompt instructs Gemini to conduct a structured interview following the 7-category taxonomy
4. Gemini asks questions, listens, follows up, extracts structured data
5. As the conversation progresses, a live preview panel shows the constitution being built in real time
6. User can pause, edit fields manually, then resume voice
7. On completion, the same multi-format export engine produces all platform exports

**Gemini Live API integration details:**
```
Endpoint: Vertex AI (us-central1 or user's preferred region)
Model: gemini-3.1-flash-live-preview (or latest stable)
Protocol: WebSocket (wss://)
Auth: Google Cloud service account or OAuth2
Audio format: PCM 16-bit, 16kHz (browser MediaRecorder)
Session duration: ~15-20 min typical
```

**System prompt structure for voice interviewer:**
The Gemini session receives a system prompt that:
- Defines the 7 taxonomy categories and their purpose
- Instructs the AI to move through categories conversationally (not rigidly)
- Requires the AI to confirm and summarize what it heard before moving on
- Outputs structured JSON alongside the conversation for real-time preview updates
- Handles graceful transitions ("Great, now let me ask about...")
- Allows the user to skip categories or come back to earlier ones

### Tier 3 — Premium Voice + Memory Router (v2, future)
- **Experience:** High-fidelity voice interview (ElevenLabs Conversational AI, ~$1.50/session) + cloud storage of your constitution + automatic sync/push to connected platforms
- **Cost to user:** $5-10/month subscription
- **Cost to operate:** ~$1.50-2.00/voice session + storage/sync infrastructure
- **Infrastructure:** ElevenLabs for voice quality, Claude as LLM brain, user account system, platform API integrations
- **Value prop:** "Your personal AI context, everywhere, always up to date."

**Memory router concept:**
- User creates an account and stores their constitution server-side
- Connects platform accounts (Claude.ai, ChatGPT, Gemini) via OAuth where available
- The router pushes constitution updates to each platform in the correct format
- Periodic review reminders ("It's been 90 days — has anything changed?")
- Version history and diffing ("Here's how your goals evolved this quarter")
- This is the recurring revenue product — but it's a separate scope and infrastructure effort

**Why ElevenLabs for premium:**
- Industry-leading voice quality and naturalness
- Drop-in browser widget (single line of HTML)
- Can use Claude as the LLM brain (best reasoning for deep interview)
- $0.10/min is reasonable for a premium tier
- WebRTC support for best echo cancellation and background noise removal

### Tier Comparison

| | Free | Voice | Premium (v2) |
|---|---|---|---|
| Builder experience | Form wizard | Voice conversation | High-fidelity voice |
| Voice engine | None | Gemini Flash Live | ElevenLabs + Claude |
| API cost/session | $0 | ~$0.35 | ~$1.50-2.00 |
| Price to user | Free | $3-5 one-time | $5-10/month |
| Multi-format export | Yes | Yes | Yes |
| Cloud storage | No (localStorage) | No (localStorage) | Yes (account-based) |
| Platform sync | No (manual export) | No (manual export) | Yes (automatic) |
| Infrastructure | Static site | Vertex AI | Full stack |
| Auth required | No | Payment only | Account + payment |

### Payment Infrastructure (Tier 2)
For the voice tier, payment processing needs to be lightweight:
- **Stripe Checkout** — session-based payment, no subscription management needed
- Flow: User clicks "Start Voice Session" → Stripe Checkout → on success, session token issued → voice session begins
- No user accounts needed — payment is per-session, stateless
- Session tokens are single-use, expire after 30 minutes of inactivity
- Alternative: Stripe Payment Links for even simpler integration (no server needed, redirect-based)

---

## Builder Experience

### Tier 1: Form-Based Wizard (Free)

A **guided conversational form** — each step presents a focused question with context about *why* it matters, optional examples, and flexible input. Not a pure chatbot, not a cold form. The prompts and tone make it feel like being interviewed by a thoughtful colleague.

### Tier 2: Voice Conversation (Paid)

A real-time voice interview powered by Gemini Flash Live via Vertex AI. The AI interviewer follows the same 7-category taxonomy but adapts to the user's responses — asking follow-up questions, reflecting back what it heard, and building the constitution collaboratively. The form wizard runs in parallel as a live preview, so the user sees their constitution taking shape as they talk. They can pause voice, manually edit any field, and resume.

Both tiers produce identical output — the same canonical document and the same platform-specific exports. The difference is the input experience, not the output.

### Flow: 7 Steps

Each step maps to one taxonomy category. Steps are sequential but non-linear (users can jump back to any completed step).

**Step 1 — Who You Are (Identity)**
- Prompt: *"Let's start with the basics. How would you introduce yourself to an AI that's going to work alongside you every day?"*
- Fields: name, role, bio (textarea with placeholder showing an example), domain expertise (tag-style input), currently learning
- Tone: warm, inviting, low-pressure

**Step 2 — What You Believe (Beliefs & Values)**
- Prompt: *"What do you hold true? These are the principles an AI should never contradict when working with you."*
- Starter suggestions (click to add, edit to personalize):
  - "Open source over proprietary when quality is comparable"
  - "Simple solutions over clever ones"
  - "Security is a process, not a product"
  - "Measure twice, cut once"
  - "Done is better than perfect" / "Quality over speed"
- Custom input: `[+ Add a belief]`
- Tone: reflective, encouraging depth

**Step 3 — Where You're Headed (Goals & Mission)**
- Prompt: *"What are you trying to accomplish? Think big picture and near-term."*
- Fields: mission statement (textarea), goals grouped by timeframe (short/medium/long), active projects (repeatable cards with name, description, status)
- Tone: forward-looking, motivating

**Step 4 — How You Work (Working Style)**
- Prompt: *"How do you actually get things done? What does a productive day look like for you?"*
- Fields: communication preference (select: concise/detailed/depends), technical environment (OS, editor, shell, languages, stack — all free text), work patterns (textarea)
- Starter suggestions for communication:
  - "Get to the point — I can ask for more detail"
  - "Give me the full picture — I'll skim what I don't need"
  - "Match the complexity to the question"
- Tone: practical, no-judgment

**Step 5 — What You Know (Knowledge & Expertise)**
- Prompt: *"Help the AI calibrate. Where are you an expert, where are you solid, and where are you learning?"*
- Three input areas with clear labels:
  - Deep expertise: "Be terse here — I know this cold"
  - Competent: "Be precise — I know the basics but get the details right"
  - Learning: "Explain thoroughly — I'm building my understanding"
- Optional: mental models / frameworks you use (tag-style input)
- Tone: empowering, non-judgmental about learning areas

**Step 6 — Rules of Engagement (Boundaries & Preferences)**
- Prompt: *"What are the ground rules? These become behavioral mandates for every AI session."*
- Three checkbox sections with pre-checked defaults + custom input:
  - **Always:** Flag security concerns, confirm before destructive actions, cite sources when uncertain, respect existing code patterns
  - **Never:** Make up information, add features not requested, use emojis unless asked, summarize what you just did
  - **When uncertain:** Say so directly, offer options with tradeoffs, ask clarifying questions
- Custom rule input for each section
- Tone: authoritative, empowering

**Step 7 — Review & Export**
- Full preview of the canonical document
- Token/character count with per-platform feasibility indicators:
  - Claude.ai: ✓ ready for import
  - CLAUDE.md: ✓ ready (shows file size)
  - ChatGPT Custom Instructions: ✓/⚠ (shows char count vs. 1,500 limit per field)
  - Gemini Gem: ✓ ready
  - etc.
- Export buttons for each platform format
- `[Download All Formats]` — ZIP file with every export
- `[Copy to Clipboard]` — copies canonical format
- Installation instructions per platform (expandable accordion)

---

## Technical Architecture

### Tier 1 Architecture (Free — Static Site)

Same pattern as the existing Enterprise Builder:
- Single-file HTML/CSS/JS (`personal.html`)
- No build process, no framework, no API calls
- Static deployment on Cloudflare Pages
- DOMPurify + marked.js for preview rendering
- localStorage persistence (key: `personal_constitution_draft`)

**New components:**
- **Multi-format export engine:** `generateExport(platform)` function that takes the canonical state and produces platform-specific output. Each platform has a formatter function.
- **Character budget display:** Live character/token counts per export format, with warnings when approaching platform limits.
- **Compression algorithm for ChatGPT:** Automatic summarization/prioritization logic that fits the full constitution into 1,500-char fields. Users can manually edit the compressed version.
- **Tag-style inputs:** For expertise areas, mental models, and tools. Comma-separated input that renders as removable pills.
- **Starter suggestion chips:** Pre-written beliefs, rules, and preferences that users click to add and then customize.

### Export Format Registry
```javascript
const EXPORT_FORMATS = {
  canonical:    { name: 'Full Document (Markdown)', ext: '.md',  fn: generateCanonical },
  claude_mem:   { name: 'Claude.ai Memory Import',  ext: '.txt', fn: generateClaudeMemory },
  claude_code:  { name: 'Claude Code CLAUDE.md',     ext: '.md',  fn: generateClaudeMD },
  chatgpt_ci:   { name: 'ChatGPT Custom Instructions', ext: '.txt', fn: generateChatGPTCI },
  chatgpt_gpt:  { name: 'ChatGPT GPT Knowledge File',  ext: '.md',  fn: generateChatGPTKnowledge },
  gemini_gem:   { name: 'Gemini Gem Instructions',   ext: '.txt', fn: generateGeminiGem },
  pai_telos:    { name: 'PAI TELOS Files',           ext: '.zip', fn: generatePAITelos },
  system_prompt:{ name: 'Raw System Prompt',         ext: '.txt', fn: generateSystemPrompt },
};
```

### Tier 2 Architecture (Voice — Vertex AI Integration)

The voice tier adds a real-time audio layer on top of the Tier 1 form wizard. Both run simultaneously — voice fills in the form, and the form produces the exports.

**Infrastructure:**
```
Browser (personal.html)
  ├── Form Wizard (Tier 1, always available)
  ├── Voice Session Manager
  │   ├── MediaRecorder API (browser mic capture)
  │   ├── WebSocket connection → Vertex AI Gemini Live API
  │   └── Audio playback (Web Audio API)
  └── Structured Data Extractor
      └── Parses Gemini responses → updates form state
```

**Vertex AI configuration:**
```
Project: user's existing GCP project
Region: us-central1 (or nearest)
Model: gemini-3.1-flash-live-preview
API: Vertex AI Live API (WebSocket)
Auth: OAuth2 (user's GCP credentials) or API key via proxy
Billing: user's existing Vertex AI billing account
```

**Key technical decisions:**

1. **Auth proxy required.** Browser cannot safely hold GCP service account keys. Options:
   - **Cloudflare Worker as auth proxy** — lightweight, pairs with existing Cloudflare Pages deployment. Worker holds the service account key, issues short-lived session tokens, proxies WebSocket connections.
   - **Firebase Auth + Vertex AI** — if already in the Google ecosystem, Firebase can handle auth and the Vertex AI call can be made via a Cloud Function.
   - **Recommended: Cloudflare Worker proxy.** Minimal new infrastructure, stays in the existing deployment stack.

2. **Structured data extraction.** Gemini's voice responses are conversational prose. To update the form, the system prompt instructs Gemini to emit structured JSON blocks alongside its spoken responses:
   ```
   [SPOKEN] "Great, so you're a cybersecurity consultant focused on OT and ICS. 
   What would you say is your core mission — the big picture reason you do this work?"
   
   [DATA] {"category": "identity", "field": "role", "value": "OT cybersecurity consultant"}
   [DATA] {"category": "identity", "field": "expertise", "value": ["OT security", "ICS", "critical infrastructure"]}
   ```
   The client parses `[DATA]` blocks from the text stream, updates `state.data`, and re-renders the form preview.

3. **Session state.** Voice sessions maintain state in both the WebSocket session context (Gemini remembers the conversation) and the client-side form state (localStorage). If the WebSocket drops, the user can reconnect and resume — the form state persists locally, and the system prompt can include a summary of what was already captured.

4. **Fallback.** If voice fails (mic permission denied, WebSocket error, API unavailable), the form wizard is always available. Voice is an enhancement, not a dependency.

**Payment flow (Stripe):**
```
User clicks "Start Voice Session"
  → Stripe Checkout (one-time payment, $3-5)
  → On success: redirect with session_id
  → Cloudflare Worker validates session_id with Stripe API
  → Worker issues a short-lived voice session token (JWT, 30-min expiry)
  → Client uses token to authenticate WebSocket proxy
  → Voice session begins
```

### Tier 3 Architecture (Premium — Future, Not v1)

Requires a full backend stack. Rough architecture for planning purposes only:

```
Client (personal.html or dedicated app)
  ↕
API Gateway (Cloudflare Workers or similar)
  ├── Auth Service (user accounts, OAuth)
  ├── Constitution Storage (R2 or PostgreSQL)
  ├── Voice Service (ElevenLabs Conversational AI)
  ├── Sync Service (platform-specific exporters)
  │   ├── Claude.ai memory import (automated paste?)
  │   ├── ChatGPT Custom Instructions (API if available)
  │   ├── Gemini Gems (API if available)
  │   └── Webhook/polling for sync status
  └── Scheduler (review reminders, version snapshots)
```

This is a separate engineering effort and likely a separate codebase/product.

---

## Design System: Warm Earth Palette

The existing site uses a dark navy/neon color scheme ("midnight command center") with critical contrast issues. The redesign moves to a warm, light-mode palette — "sunlit study" — that improves readability, feels calmer and more human, and works across both the enterprise builder and the new personal constitution page.

### Current Problems

**Low background contrast:** The four background tokens (`#0a0e17`, `#0d1929`, `#111f36`, `#0b1322`) are nearly indistinguishable — only ~4 luminance points apart. Cards, panels, and inputs all blend into the page.

**Failing text contrast:**
| Token | Current Hex | Contrast vs background | WCAG AA |
|---|---|---|---|
| `--text-primary` | `#f0f4f8` | ~15:1 | Pass |
| `--text-secondary` | `#8a9bb0` | ~5.5:1 | Borderline |
| `--text-muted` | `#5e7089` | ~3.2:1 | **Fail** (requires 4.5:1 for body text) |

`--text-muted` is used heavily (form hints, footer, stats, tags, step counts) and fails WCAG AA. The neon accent colors (blue `#3b82f6`, purple `#8b5cf6`, teal `#64c9cf`) contribute to a sci-fi aesthetic that doesn't match the product's purpose — governance, thoughtfulness, personal reflection.

### Typography — Unchanged

The font stack is strong and aligns well with the new direction:
- **Fraunces** (display/headings) — distinctive optical-size serif with organic, warm character
- **DM Sans** (body) — clean, readable geometric sans
- **JetBrains Mono** (code/data) — excellent monospace

Fraunces in particular has the earthy quality the new palette calls for — it was being used against the wrong backdrop.

### New Design Tokens

```css
:root {
  /* ── Backgrounds ── */
  --bg-root:      #f6f1eb;   /* warm parchment — the page itself */
  --bg-surface:   #ffffff;   /* clean white — cards, panels */
  --bg-elevated:  #faf7f3;   /* barely warm — elevated surfaces */
  --bg-input:     #f0ebe4;   /* sandy — input fields */
  --border:       #d9cfc3;   /* warm taupe border */
  --border-subtle: rgba(120,100,80,0.08);

  /* ── Text ── */
  --text-primary:   #2c2418;  /* dark espresso — headings, body */
  --text-secondary: #5c4f3e;  /* warm walnut — descriptions */
  --text-muted:     #8a7e6f;  /* dusty clay — hints, labels */
  --text-bright:    #3d3225;  /* rich bark — emphasized text */
  --text-inverse:   #faf7f3;  /* for use on dark accent buttons */

  /* ── Accent: Primary (forest sage) ── */
  --sage:       #5a7a64;
  --sage-dim:   rgba(90,122,100,0.10);
  --sage-glow:  rgba(90,122,100,0.20);
  --sage-text:  #4a6853;

  /* ── Accent: Secondary (warm clay) ── */
  --clay:       #b07850;
  --clay-dim:   rgba(176,120,80,0.10);
  --clay-glow:  rgba(176,120,80,0.18);
  --clay-text:  #96633f;

  /* ── Accent: Tertiary (deep indigo — for depth) ── */
  --indigo:       #4a5578;
  --indigo-dim:   rgba(74,85,120,0.10);
  --indigo-glow:  rgba(74,85,120,0.18);
  --indigo-text:  #3d4766;

  /* ── Enterprise tier colors (muted versions) ── */
  --blue:        #4a6fa5;     /* muted blue-steel */
  --blue-dim:    rgba(74,111,165,0.10);
  --blue-glow:   rgba(74,111,165,0.18);
  --blue-text:   #3b5d8f;

  --purple:      #7b6b99;     /* dusty lavender */
  --purple-dim:  rgba(123,107,153,0.10);
  --purple-glow: rgba(123,107,153,0.18);
  --purple-text: #6a5b87;

  --teal:        #5a8a7a;     /* forest teal */
  --teal-dim:    rgba(90,138,122,0.10);
  --teal-glow:   rgba(90,138,122,0.18);
  --teal-text:   #4a7768;

  /* ── Active tier (set by JS, default to sage) ── */
  --tier-color: var(--sage);
  --tier-dim:   var(--sage-dim);
  --tier-glow:  var(--sage-glow);
  --tier-text:  var(--sage-text);

  /* ── Status ── */
  --amber:  #c4883a;
  --red:    #b85450;
  --red-dim: rgba(184,84,80,0.10);
  --green:  #5a8a5e;

  --gauge-ok:     var(--sage);
  --gauge-warn:   #c4883a;
  --gauge-danger: #b85450;

  /* ── Typography (unchanged) ── */
  --font-display: 'Fraunces', Georgia, serif;
  --font-body:    'DM Sans', system-ui, sans-serif;
  --font-mono:    'JetBrains Mono', 'Consolas', monospace;
  --radius:    8px;
  --radius-lg: 12px;
  --ease: cubic-bezier(0.16, 1, 0.3, 1);
}
```

### Contrast Verification (against `--bg-root: #f6f1eb`)

| Token | Hex | Contrast Ratio | WCAG AA |
|---|---|---|---|
| `--text-primary` | `#2c2418` | ~12.5:1 | Pass |
| `--text-secondary` | `#5c4f3e` | ~6.5:1 | Pass |
| `--text-muted` | `#8a7e6f` | ~3.7:1 | Pass (large text/UI elements) |
| `--sage` | `#5a7a64` | ~4.7:1 | Pass |
| `--clay` | `#b07850` | ~3.8:1 | Pass (large text/UI elements) |

### Component-Level Changes

**Remove dot grid overlay:**
```css
/* DELETE the current body::before sci-fi dot grid */
/* Optionally replace with subtle paper grain texture at 3% opacity */
```

**Topbar — warm transparent:**
```css
.topbar {
  background: rgba(246,241,235,0.92);
  backdrop-filter: blur(16px);
  border-bottom: 1px solid var(--border);
}
```

**Cards — soft shadows instead of border-only:**
```css
.panel, .project-card {
  background: var(--bg-surface);
  border: 1px solid var(--border);
  box-shadow: 0 1px 3px rgba(44,36,24,0.06), 0 4px 12px rgba(44,36,24,0.04);
}
.project-card:hover {
  box-shadow: 0 4px 20px rgba(44,36,24,0.10);
  border-color: var(--clay);
}
```

**Hero glow — warm light instead of neon:**
```css
.hero::before {
  background: radial-gradient(ellipse, rgba(176,120,80,0.08) 0%, transparent 70%);
}
```

**CTA buttons — earthy accents:**
```css
.hero__cta { background: var(--sage); color: var(--text-inverse); }
.hero__cta:hover { box-shadow: 0 8px 24px var(--sage-glow); }
.hero__cta.tier-2 { background: var(--indigo); }
.hero__cta.tier-3 { background: var(--clay); }
```

**Form focus states:**
```css
.form-input:focus {
  border-color: var(--tier-color);
  box-shadow: 0 0 0 3px var(--tier-dim);
}
```

### Page-Specific Accents

| Page | Primary Accent | Rationale |
|---|---|---|
| Enterprise builder (`index.html`) | `--sage` (forest sage) | Institutional, grounded, trustworthy |
| Personal builder (`personal.html`) | `--clay` (warm clay) | Personal, crafted, human, hands-on |
| Deploy guide (`deploy.html`) | `--indigo` (deep indigo) | Technical, precise, operational |
| Projects (`projects.html`) | Per-project accent colors | Variety, visual distinction between projects |

### Migration Path

The palette swap is a **CSS-only operation**. Every color change maps 1:1 to existing CSS custom property names — only the values change.

Steps:
1. Update `:root` variables in `index.html`, `deploy.html`, `projects.html`
2. Update hardcoded `rgba()` values in inline styles (hover states, badge backgrounds)
3. Remove `body::before` dot grid
4. Add soft `box-shadow` to `.panel` and `.project-card`
5. Update `.topbar` background to warm-transparent
6. No structural HTML or JS changes required

---

## Site Integration

### URL Structure
```
constitutionbuilder.ai/              ← mode selector (enterprise vs. personal)
constitutionbuilder.ai/personal      ← Personal AI Constitution builder
constitutionbuilder.ai/deploy        ← unchanged (enterprise deployment guide)
constitutionbuilder.ai/projects      ← unchanged
```

### Landing Page Changes (index.html)
Add a mode selector hero above the existing enterprise wizard:
- **Enterprise Constitution** card → starts existing wizard
- **Personal AI Constitution** card → navigates to `/personal`

### Navigation
Add "Personal" link to the nav bar on all pages.

### Sitemap
Add `personal.html` entry.

---

## Implementation Roadmap

### v1.0 — Free Form Wizard + Multi-Platform Export
- **Warm Earth palette redesign** across all existing pages (CSS-only, no structural changes)
- `personal.html` with 7-step form wizard (built with new palette from the start)
- All 8 export formats functional
- Mode selector on index.html landing page
- Nav link updates across all pages
- Sitemap update
- **Ship target:** Can be built and deployed with zero infrastructure changes

### v1.5 — Voice Conversation (Gemini Flash Live)
- Cloudflare Worker auth proxy for Vertex AI
- WebSocket voice session manager in `personal.html`
- Structured data extraction from Gemini responses
- Stripe Checkout integration for per-session payment
- Voice + form run in parallel (voice fills the form)
- **Ship target:** Requires Cloudflare Worker + Stripe account + Vertex AI project

### v2.0 — Premium Voice + Memory Router
- User accounts and constitution cloud storage
- ElevenLabs Conversational AI integration (Claude as LLM brain)
- Platform sync service (auto-push to connected AI tools)
- Version history and quarterly review reminders
- **Ship target:** Separate product/codebase, significant infrastructure

### Future Enhancements (any tier)

1. **Import from existing memories.** Reverse the flow — paste your ChatGPT memory export or Claude memories, and the tool structures them into a constitution.

2. **Community templates.** Pre-built constitutions for common roles (security engineer, data scientist, product manager, student, writer, executive) as starting points.

3. **Version diffing.** Track changes between constitution versions — "here's how your goals evolved this quarter."

4. **API endpoint.** A simple API that returns your constitution in any format, for programmatic integration into AI workflows.

5. **Text-based conversational mode.** A chat interface (cheaper than voice) that interviews you via text. Could use Gemini Flash or Claude Haiku for very low cost. Middle ground between form and voice.

---

## Open Questions

1. **Should the free tier require sign-up?** Current thinking: No. Same as the enterprise builder — pure client-side, no accounts, no data leaves the browser. localStorage for persistence, export for portability. Accounts only enter the picture at Tier 3.

2. **How to handle the ChatGPT compression?** The 1,500-character limit is brutal. Options: (a) auto-compress with a prioritization algorithm, (b) let the user manually edit the compressed version, (c) both — auto-compress with manual override. Leaning toward (c).

3. **PAI TELOS export — how faithful?** Should the TELOS export match PAI's file structure exactly (for drop-in compatibility), or produce a simplified version? Recommend exact compatibility — it's the power-user path and Daniel's community would appreciate interop.

4. **Should the "About This Document" section explain what a Personal AI Constitution is?** Including a brief explainer in the output helps if someone shares their constitution with a colleague or posts it publicly. But it adds tokens. Recommend: include it in the canonical format, strip it from platform-specific exports.

5. **Voice session pricing.** $3-5/session is the proposed range. At ~$0.35 cost, that's healthy margin. But is the value clear enough for users to pay? Consider: a "try 2 minutes free" demo mode using Gemini's free tier, then prompt for payment to continue the full session.

6. **Cloudflare Worker vs. Cloud Function for auth proxy.** Worker stays in the existing Cloudflare ecosystem (simpler). Cloud Function stays in the Google ecosystem (closer to Vertex AI). The Worker is recommended for v1.5 since the site already deploys on Cloudflare Pages, but either works.

---

## Reference Links

- Live site: https://constitutionbuilder.ai/
- GitHub repo: https://github.com/HillviewCap/enterprise-ai-constitution
- Daniel Miessler's PAI: https://github.com/danielmiessler/Personal_AI_Infrastructure
- Claude.ai memory import: https://support.claude.com/en/articles/12123587-import-and-export-your-memory-from-claude
- Claude Code memory docs: https://docs.anthropic.com/en/docs/claude-code/memory
- ChatGPT Custom Instructions: Settings > Personalization in ChatGPT
- Gemini Gems: gemini.google.com (Gemini Advanced required)
- CC BY 4.0 License: https://creativecommons.org/licenses/by/4.0/
