# Exodon Architecture — Initial Blueprint

## Architectural Goal

Keep the public website, internal AI Development Studio, and client systems conceptually separate.

## System 1 — ExodonProfits.com

Purpose:
Customer-facing marketing, education, qualification, and project intake.

Responsibilities:
- public content
- case studies
- service explanation
- intake forms
- consultation CTA
- analytics

It should not contain the full internal agent orchestration system.

## System 2 — Exodon AI Development Studio

Purpose:
Internal project delivery system.

Future capabilities may include:
- project records
- research artifacts
- PRDs
- architecture documents
- agent coordination
- GitHub issues
- QA status
- approvals
- deployment status

This should be built only after the manual workflow is proven.

## System 3 — Client Smart Layers

Each client implementation may combine:
- reusable Exodon Core
- industry modules
- client configuration
- custom client features
- supported integrations
- AI agents

## Reuse Strategy

```text
EXODON CORE
    +
INDUSTRY MODULES
    +
CLIENT CONFIGURATION
    +
CLIENT-SPECIFIC FEATURES
```

## Candidate Exodon Core Modules

### Identity
- organizations
- users
- roles
- permissions
- authentication

### Operations
- tasks
- notifications
- documents
- dashboards
- reporting
- activity history

### Integration
- API connectors
- webhooks
- scheduled sync
- imports / exports

### AI
- agent framework
- tool permissions
- knowledge access
- approval workflow
- logging

## Architecture Principles

- simple before complex
- monolith before microservices unless justified
- modular boundaries
- least privilege
- environment separation
- migrations for database changes
- observable systems
- documented integrations
- reusable components

## Integration Decision Tree

For any third-party application:

1. Does an official API exist?
2. Does it support the required data/actions?
3. Are webhooks available?
4. Is OAuth required?
5. Is supported export/import sufficient?
6. Can approved middleware solve the gap?
7. If none apply, should the Exodon system simply work alongside the software?

Never fabricate an integration method.
