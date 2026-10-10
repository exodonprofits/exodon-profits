# Architecture Run 001 — Exodon Profits 2.0

## Status
COMPLETE — READY FOR UX/UI HANDOFF

## Purpose
Define the technical architecture for Exodon Profits Project #001 while preserving the approved strategy:

**Keep what works. Build what's missing. Automate what slows you down.**

This architecture intentionally keeps the first release small and defers the full autonomous AI Development Studio until the manual seven-agent workflow is proven.

---

# 1. Architecture Decision Summary

Exodon should be organized as four separate layers:

1. **ExodonProfits.com** — public customer-facing website
2. **Exodon Project Intake / Discovery Layer** — captures qualified opportunities
3. **Client Smart Layers** — isolated client-specific systems
4. **Exodon AI Development Studio** — future internal operating system, deferred

These layers should share standards and reusable components, but they should not be built as one tightly coupled application.

---

# 2. System Context

```text
                     PROSPECT / CLIENT
                           |
                           v
                  EXODONPROFITS.COM
                           |
             +-------------+-------------+
             |                           |
             v                           v
       Learn / Case Studies       Start Discovery
                                         |
                                         v
                              PROJECT INTAKE / CRM
                                         |
                                         v
                                EXODON PROJECT TEAM
                                         |
                    +--------------------+--------------------+
                    |                    |                    |
                    v                    v                    v
                DISCOVER               BUILD              AUTOMATE
                    |                    |                    |
                    +--------------------+--------------------+
                                         |
                                         v
                                CLIENT SMART LAYER
                                         |
                         +---------------+---------------+
                         |               |               |
                         v               v               v
                  Existing Software   Custom App      AI / Automation
```

---

# 3. Phase 1 Architecture — Build Now

The first production release should include only:

## Public Website
- Home
- Smart Layer explanation
- Discover / Build / Automate
- Victoria Nails case study
- Services / solution examples
- Project-fit qualification
- Discovery intake
- Contact / consultation CTA
- Privacy / terms
- Analytics

## Intake System
Capture:
- business name
- contact
- industry
- company size
- current software
- operational pain
- manual workflows
- desired outcome
- urgency
- budget range if appropriate
- permission to follow up

## Basic Internal Handling
Do not build a large internal project platform yet.

Initially use:
- GitHub
- structured project documents
- existing communication tools
- simple CRM/intake storage
- manual seven-agent workflow

---

# 4. Recommended Technology Direction

The exact implementation should respect the existing website codebase after repository audit.

For a new or substantially rebuilt site, preferred direction:

## Frontend
- modern React-based web framework
- server-rendered / SEO-friendly pages
- responsive-first design
- component-based design system

## Backend
Use backend capabilities only where required:
- intake submission
- email / notification workflow
- analytics events
- future authenticated client portal

## Database
Use Supabase/Postgres if Exodon needs structured intake and project data.

Initial entities may include:
- organizations
- contacts
- discovery_submissions
- projects
- project_status
- notes
- metrics_baselines
- integrations
- audit_events

Do not create a large multi-tenant schema before it is needed.

---

# 5. Identity and Access

## Public Website
No login required.

## Future Client Portal
Use organization-scoped authentication.

Roles may include:
- client_owner
- client_manager
- exodon_admin
- exodon_project_manager
- exodon_developer
- exodon_reviewer

## Security Principle
Every authenticated record must belong to a defined organization / project scope.

Avoid shared unrestricted access across clients.

---

# 6. Client Isolation Model

Client Smart Layers must be logically isolated.

Preferred options:

### Option A — Separate Deployment / Project Per Client
Best default for early custom work.

Benefits:
- strong isolation
- simpler troubleshooting
- easier ownership boundaries
- safer custom logic
- easier client-specific deployment

### Option B — Shared Multi-Tenant Platform
Use only after repeated patterns are proven.

Do not force early clients into one shared application merely to appear scalable.

## Architect Recommendation
Start with **isolated client projects**, while extracting reusable packages and templates into Exodon Core.

---

# 7. Exodon Core Strategy

Exodon Core should begin as a library of reusable patterns and modules, not as one giant platform.

Potential reusable areas:

```text
EXODON CORE

Identity
├── Auth patterns
├── Organization model
├── Roles
└── Permissions

Operations
├── Tasks
├── Notifications
├── Documents
├── Audit logs
└── Reporting patterns

UI
├── Dashboard shell
├── Navigation
├── Tables
├── Forms
├── Status components
└── Responsive patterns

Integration
├── API client patterns
├── Webhook handlers
├── Sync jobs
└── Import/export utilities

AI
├── Prompt patterns
├── Human approval patterns
├── Tool permission model
├── Audit / trace patterns
└── Fallback behavior
```

Do not extract a component into Core merely because it appears once.

A good rule:
**reuse after repetition, not before evidence.**

---

# 8. Client Smart Layer Pattern

Each client implementation should conceptually contain three layers:

```text
Reusable Exodon Core
        +
Industry / Workflow Modules
        +
Client-Specific Configuration & Logic
        =
Client Smart Layer
```

Example:

```text
Exodon Core
   +
Salon Operations Module
   +
Victoria Nails Rules
   =
Salon Genie
```

This supports the 80/20 architecture goal without pretending all clients are identical.

---

# 9. Integration Architecture

For every third-party system, classify the relationship as:

1. KEEP
2. CONFIGURE
3. INTEGRATE
4. CUSTOMIZE AROUND
5. BUILD NEW

Supported integration mechanisms may include:
- public API
- vendor-approved private API
- OAuth
- webhook
- scheduled synchronization
- supported export/import
- middleware
- manual exchange where necessary

## Rule
If a supported connection has not been verified, Exodon must say:

**“Works alongside [software].”**

Do not say:

**“Integrates with [software].”**

until verified.

---

# 10. AI Architecture

AI must remain an optional capability, not the foundation of every workflow.

## Low-Risk
AI may act automatically.

Examples:
- summaries
- categorization
- draft generation

## Medium-Risk
AI may act if:
- action is logged
- action is reversible
- permissions are constrained

## High-Risk
AI recommends; human approves.

Examples:
- sensitive customer communication
- financial actions
- destructive operational changes

## Critical
Human only.

## Required AI Controls
- scoped tool permissions
- explicit organization context
- audit trail
- fallback behavior
- uncertainty handling
- human approval gates
- no secret leakage
- no unrestricted production access

---

# 11. Data Architecture Principles

Use:
- explicit organization_id / project_id boundaries
- foreign-key constraints
- least privilege
- audit events for important changes
- migration-based schema changes
- staging before production

Avoid:
- storing client data in generic unscoped tables
- sharing production credentials across projects
- direct client-side privileged database access
- silent destructive migrations

---

# 12. Repository Strategy

## Exodon Parent Repository
`exodon-profits`

Should contain:
- company strategy
- agent prompts
- website
- architecture
- templates
- public site code
- future Studio code if appropriate

Suggested structure:

```text
exodon-profits/
├── docs/
├── agents/
├── decisions/
├── templates/
├── website/
├── studio/
└── shared/
```

## Client Repositories
Prefer separate repositories for client systems during the early stage.

Example:

```text
victoria-nails-salon-genie
client-a-smart-layer
client-b-operations
```

Reusable code should be promoted into Exodon Core only when it becomes genuinely reusable.

---

# 13. Environment Strategy

Every meaningful software project should have:

## Development
Local / developer environment.

## Staging
Client-safe testing environment.

## Production
Approved live system.

Flow:

```text
Feature Branch
     ↓
Review
     ↓
Tests
     ↓
Staging
     ↓
QA
     ↓
Human Approval
     ↓
Production
```

No meaningful production deployment should bypass QA and human approval.

---

# 14. Future AI Development Studio

The Studio is **not Phase 1**.

Its future role is to orchestrate:
- intake
- research
- PRDs
- architecture
- tasks
- GitHub work
- agent assignments
- approvals
- QA
- deployment tracking

The Studio should not become:
- the client's runtime application
- the only source of project truth
- a replacement for GitHub
- a giant shared database containing unrestricted client data

## Studio Boundary

```text
AI DEVELOPMENT STUDIO
      |
      +-- reads project context
      +-- coordinates agents
      +-- creates / tracks tasks
      +-- links to GitHub
      +-- records approvals
      +-- tracks project state

CLIENT APP
      |
      +-- runs independently
      +-- has isolated data
      +-- has its own production lifecycle
```

---

# 15. Security Model

Minimum standards:

- secrets stored in secure environment configuration
- least-privilege service roles
- separate production / staging credentials
- row-level security where multi-tenant data exists
- secure session handling
- validation of all external input
- audit logging for sensitive actions
- rate limiting where appropriate
- no client cross-data access
- no AI agent with unrestricted production permissions

---

# 16. Website Architecture

Recommended high-level route model:

```text
/
├── /smart-layer
├── /discover
├── /build
├── /automate
├── /case-studies
│   └── /victoria-nails
├── /services
├── /how-it-works
├── /start-discovery
├── /about
├── /contact
├── /privacy
└── /terms
```

The UX Designer may simplify or combine these routes.

Architecture should not dictate unnecessary pages.

---

# 17. Discovery Intake Flow

Recommended initial flow:

```text
Visitor
  ↓
Start Discovery
  ↓
Basic business info
  ↓
Current software
  ↓
Operational pain
  ↓
Manual / duplicate work
  ↓
Desired outcome
  ↓
Fit qualification
  ↓
Submit
  ↓
Create discovery record
  ↓
Notify Exodon
  ↓
Manual review
```

Do not automate proposal generation or pricing in Phase 1.

---

# 18. Analytics Requirements

Track:
- CTA clicks
- discovery starts
- discovery completions
- case-study engagement
- service-page engagement
- consultation requests
- lead source
- conversion from Discovery to paid Blueprint
- conversion from Blueprint to Build

Avoid collecting unnecessary sensitive information.

---

# 19. Architecture Decisions

## ADR-A
**Use a service-led architecture, not SaaS-first.**

## ADR-B
**Keep client systems isolated during the early stage.**

## ADR-C
**Build Exodon Core incrementally from repeated patterns.**

## ADR-D
**Defer full AI Development Studio automation.**

## ADR-E
**GitHub remains the source of truth for approved project artifacts and code.**

## ADR-F
**AI actions are permissioned according to risk.**

## ADR-G
**No unverified third-party integration claims.**

---

# 20. Phased Technical Roadmap

## Phase 1 — Public Presence
Build:
- Exodon website
- case study
- service pages
- Discovery intake
- analytics
- simple data capture / notification

## Phase 2 — Delivery Standardization
After first real clients:
- standard project templates
- reusable UI shell
- reusable auth patterns
- reusable organization / role model
- reusable integration patterns
- reusable AI approval pattern

## Phase 3 — Exodon Core
Only after repetition is proven:
- formal shared packages
- industry modules
- integration library
- internal deployment standards

## Phase 4 — AI Development Studio
Build the internal orchestration layer after the manual process produces enough evidence about what should actually be automated.

---

# 21. Technical Risks

1. Premature multi-tenancy
2. Overbuilding Exodon Core
3. Coupling the public site to internal operations
4. Building the Studio before validating demand
5. Unsupported third-party integrations
6. Cross-client data exposure
7. Excessive custom forks
8. AI agents gaining too much authority
9. Vendor lock-in without exit strategy
10. Lack of measurable client outcomes

---

# 22. Architect Decision

**PROCEED TO UX/UI**

The product strategy is technically feasible.

No major architecture blocker exists.

The recommended first implementation remains intentionally small:

**ExodonProfits.com + Discovery intake + Victoria Nails proof + basic operational lead capture.**

Do not build the full Studio or generalized multi-tenant Exodon platform yet.

---

# 23. Handoff to UX/UI Designer

The UX/UI Designer should now define:

1. information architecture
2. homepage hierarchy
3. Smart Layer explanation
4. Discover / Build / Automate presentation
5. Victoria Nails case-study experience
6. Discovery intake UX
7. mobile / desktop responsive behavior
8. design-system direction
9. trust / proof structure
10. CTA strategy

The design must:
- speak in business language rather than technical jargon,
- explain the Smart Layer visually,
- emphasize measurable outcomes,
- avoid generic “AI agency” aesthetics,
- feel like a modern business application company,
- preserve a clear path to Start Discovery.

## Status
COMPLETE

## Next Agent
UX/UI Designer — Formal Run 001
