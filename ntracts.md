# Ntracts

## Company Overview

Ntracts is a healthcare-focused governance, risk, and compliance (GRC) software company. The platform is organized around multiple solution areas and positioned as healthcare-specific rather than industry-agnostic. Key positioning: 98% client retention, KLAS-recognized healthcare CLM, unified governance platform.

## Product Architecture

Four solution pillars:

- **CLM Tract** - contract lifecycle management
- **Policy Tract** - policy and procedure management (formerly MCN / ellucid Policy Manager)
- **Compliance Tract** - compliance, auditing, and monitoring workflows (formerly Compliatric)
- **Physician Tract** - physician onboarding, compensation, and related governance

## 2026 Product Strategy

Each product must win independently for its target market before bundling becomes the play. CLM Tract and Policy Tract should win independently for mid-market and enterprise buyers. Compliance Tract is the all-in-one answer for smaller teams.

## Acquisition Context

Ntracts acquired MCN Solutions in 2025. MCN and Compliatric integration is a recurring company theme with explicit urgency around cross-company integration and reducing vendor sprawl. Integration is directionally real but operationally incomplete.

## Tech Stack and Architecture

### CLM Stack
- Azure-centric hosting and infrastructure
- .NET application stack
- Snowflake as analytics/reporting warehouse
- Omni as new reporting/analytics layer (replacing Exago)
- Fivetran for replication into Snowflake
- DBT for Snowflake schema/views/functions
- GitHub Enterprise for source control
- Azure Front Door in platform edge architecture
- Elastic Pool usage in Azure SQL footprint
- OnlyOffice for in-app document editing
- Auth0 being considered/adopted for identity
- Bicep favored over raw ARM for Azure IaC going forward

### Policy Stack
- PHP monolith moving from CodeIgniter to Symfony 7.2 / PHP 8.5
- AWS infrastructure
- Doctrine ORM
- OnlyOffice for document editing
- Elasticsearch (moving toward AWS OpenSearch)
- MySQL database

### Reporting Architecture
- Operational systems in Azure SQL (CLM) / MySQL (Policy)
- Replication into Snowflake through Fivetran
- DBT-managed schema/view layer in Snowflake
- Omni on top of Snowflake for reporting, dashboards, AI-enabled analytics
- Exago being replaced - migration complexity around report parity and user expectations

### Data Architecture Themes
- Medallion architecture discussed for Omni/Snowflake
- Topic modeling central to Omni reporting design
- Row-level security through passed user IDs/sessions
- Client-defined fields are a recurring architectural pain point
- Data validation emerging as foundational platform capability

### Identity and Access
- Azure SSO core in CLM
- Auth0/OAuth future direction
- SCIM discussed for future cross-product provisioning
- Unified SSO across products is an explicit product proposal

## Leadership

- **David Paschall** - CEO
- **Emily Danek** - Chief of Staff
- **Stephanie Haywood** - Chief Client Officer
- **Lily He** - Chief Product Officer
- **Sara Low** - Chief Operating Officer
- **Jason Marsh** - VP of Information Security & Technology
- **Glenn Orr** - CTO (Tom's direct report-to)
- **Joyce Paich** - SVP, Nursing & Professional Services
- **Nate Reveley** - Chief Innovation Officer
- **Dave Roberts** - CFO
- **Dale Van Gorder** - Chief Sales Officer

## Engineering Team

- **Ajay Pratap Meena** - roadmap/delivery/grooming/cross-functional product-engineering coordination
- **Brian Griffith** - key engineering lead on UI, embedding, OnlyOffice, Omni-related work
- **Richard Kevern** - architecture, data validation, backlog rigor, systemic quality
- **Rich Puskarich** - most senior engineer, deep legacy and infra knowledge, pragmatic, cowboy tendency, high production scar tissue, wants more intentional engineering contribution
- **Michael Troyer** - tenant admin, data load, release pipeline, delivery mechanics
- **Eddie Wuerch** - Snowflake/Omni/data/SQL/reporting backbone, deep Salesforce and SQL background
- **Billy Koliba** - AI/clause analysis/abstraction
- **Andrew Campbell** - reports, Exago/Omni transition, admin-heavy delivery work
- **Isaac Cocar** - UI and auto-renewal work
- **Eric Chreist** - QA/testing/release alignment
- **Amanda** - implementation/migration/customer delivery pressure
- **Hannah Turpin** - key business stakeholder on AbstractIQ/data abstraction
- **Nicholas Cruz** - support engineer with growing DevOps/cloud/platform interests, good investment for pipeline/Azure growth
- **Jonathan Tuley** - support engineer, growing in Playwright and QA automation
- **Sarah Parent, Karlee Wright** - support prioritization escalation path

## Current Priorities

### Top Portfolio Priorities

1. **Omni + Snowflake** - biggest architectural and product transition. Replace Exago, embed Omni, solve permissions/CDF/deployment patterns, provide AI-enabled analytics.
2. **AbstractIQ / ExtractIQ / Project 10** - AI-powered abstraction acceleration. Faster, scalable data abstraction and QA for implementations. Tied to implementation economics.
3. **Data Validation** - common UI and API validation layer. Foundation for broader API strategy.
4. **Physician Contracts API** - new revenue/strategic vertical. Pass contract data into physician comp systems.
5. **OnlyOffice upgrade and containerization** - reliability and editing bug fixes.
6. **AI rollout (Project Force Multiplier)** - leadership-first rollout, ambassadors, governance, measurable business impact.

### CLM Tract Initiatives
- Workflow flexibility, DocJuris integration UX, data validation (UI & API), infrastructure updates, Azure Front Door, Physician Contracts API, Omni & Snowflake, Project 10 Bulk Abstraction QA Tool

### Compliance Tract Initiatives
- Automated code quality testing, Playwright regression, Subscription Management Phase 2, Surveys Builder/Form Revamp, Compliance Core Console, UI theme refresh, role-based apps, Compliance Sets, Auditing & Monitoring, Module AI stretch work

### AI Tools Team Initiatives
- Clause Search, clause analyzer accuracy, ingest pipeline, cost reduction, Snowflake views/Omni topics for clause testing, bulk policy abstraction support

## Key Decisions

- **Omni replaces Exago** - better UX, AI-enabled analytics, scalable cross-company reporting
- **Omni report creation limited to Ntracts Admins first** - reduces permission complexity, matches actual usage patterns
- **Data validation is foundational** - prerequisite for scaling platform data movement safely
- **AbstractIQ is MVP-first** - ship core value, iterate on accuracy
- **2026 work must ladder to independent product wins** - bundling only works if each product is already compelling
- **Snowflake for reporting, not production DBs** - scale, performance isolation, safer analytics
- **Bicep over raw ARM** - more modern, readable, pipeline-friendly
- **Stop recording standups** - was hurting trust and openness

## Strategic Through-Line

The long bet is healthcare-specialized data quality, governance-ready workflows, reporting and search built on cleaner structured data, fewer vendors for customers, and a platform that can support cross-product intelligence without collapsing under its own history.

## Company Pain Patterns

- Roadmap ambiguity and weak prioritization hygiene
- Legacy drag from V2/older systems
- Architecture work that business sees as "why does this take so long?"
- Platform changes during acquisition integration
- AI initiatives with real promise but slippery requirements
- Support noise and migration work stealing oxygen from strategic work
