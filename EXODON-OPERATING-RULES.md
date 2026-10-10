# Exodon Operating Rules

## Purpose

This document defines the shared rules that every Exodon agent, developer, contractor, and future automation must follow.

## 1. Business First

Do not begin with technology.

First understand:
- the business problem
- the users
- the current workflow
- the existing software
- the cost of the problem
- the desired business outcome

## 2. Keep What Works

Existing software should not be replaced simply because Exodon can build an alternative.

For every major capability, evaluate:

1. Keep
2. Configure
3. Integrate
4. Customize around
5. Build new

Custom development is the last option, not the first.

## 3. Smart Layer Principle

Exodon specializes in filling the gap between a client's existing software and the way the client's business actually operates.

The Exodon Smart Layer may include:
- custom web applications
- internal tools
- dashboards
- workflow systems
- integrations
- AI agents
- automation
- business intelligence

## 4. 80/20 Architecture Goal

Where practical, target:

- 80% reusable Exodon components, modules, infrastructure, or patterns
- 20% client-specific customization

This is a strategic goal, not a rigid formula.

## 5. No Unverified Integration Claims

Do not claim that Exodon integrates directly with a third-party product unless the integration method has been verified.

Supported methods may include:
- public API
- private approved API
- webhook
- OAuth
- supported data export/import
- approved middleware

If no supported integration is confirmed, say that the Exodon system works alongside the existing software.

## 6. Human Approval Gates

Human Product Owner approval is required for:
- major new projects
- major changes in business model
- destructive data migrations
- production deployment
- significant budget commitments
- high-risk automation
- major scope changes

## 7. AI Risk Levels

### Low Risk
AI may act automatically.

Examples:
- summarization
- internal categorization
- draft generation

### Medium Risk
AI may act automatically if actions are logged and reversible.

### High Risk
AI recommends. Human approves.

Examples:
- customer-facing financial decisions
- destructive data changes
- sensitive communications

### Critical
Human only.

## 8. Security by Default

Never:
- store production secrets in source code
- bypass authentication
- disable authorization for convenience
- expose client data across organizations
- allow unrestricted database access

Use least privilege.

## 9. Staging Before Production

All meaningful changes should pass through a development or staging environment before production.

## 10. Source of Truth

GitHub is the source of truth for:
- product requirements
- architecture
- agent instructions
- implementation status
- design decisions
- release history

Important decisions should not live only in chat.

## 11. Documentation Is Part of the Product

A feature is not complete until relevant documentation is updated.

## 12. Minimal-Diff Development

Prefer the smallest coherent change that meets the approved requirement.

Avoid large rewrites unless clearly justified.

## 13. Agent Independence

The QA / Reviewer must review work independently from the Developer.

The Research Agent must challenge ideas rather than automatically validate them.

## 14. No AI for AI's Sake

AI should be added only when it:
- saves meaningful time
- reduces cost
- improves accuracy
- improves customer experience
- creates capabilities that are otherwise difficult to deliver

## 15. Client Outcome

Every project should identify measurable outcomes where possible, such as:
- fewer manual steps
- fewer missed leads
- faster service
- reduced administrative time
- fewer errors
- higher conversion
- better visibility
- lower operating cost
