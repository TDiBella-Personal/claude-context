# MCN (Policy Tract)

## What MCN Is

MCN is a document-centric compliance platform for organizations that need to manage policies, procedures, approvals, audit trails, training, and regulatory updates in a defensible way. It serves regulated organizations with heavy compliance demands - historically strongest in healthcare but with stated expansion beyond.

Internally being rebranded as **Policy Tract**. Customers still commonly call it MCN, ellucid Policy Manager, or Policy Manager.

## Product Family

The product family is broader than a single app:

- **Policy Manager** - policy lifecycle: centralized storage, versioning, approvals, attestation, reporting. Center of gravity for current risk.
- **Policy Library** - prebuilt policy/procedure content
- **StayAlert** - regulatory update tracking and compliance alerts. StayAlert Plus ("Steve") was intended to map regulatory changes to impacted client policies but is back-burnered.
- **LMS/eLearning** - training and competency support
- **Contract Manager** - broader ecosystem around policy
- **USM** - user/permission management

## Target Customer

Organizations with real compliance overhead and long-lived operational dependency. Key examples: hospitals, health systems, universities. Customers care about auditability, bulk administrative actions, accessibility compliance, reporting, and reliability.

## Current Product Capabilities and Gaps

### Approvals and Workflow
Workflows are essentially tasks with approval groups. Group-based, not per-user. Has alternate paths like quick approve and click edit for emergency bypass. Current capability is narrower than customers want - future demand for evaluation workflows, review-only steps, rule-based approvals.

### Search
Known weak point. Ramona explicitly called it out. Current effort is incremental tuning on antiquated Elasticsearch, with longer-term movement toward AWS OpenSearch. Tied directly to user dissatisfaction and retention risk.

### Mass Actions
Major near-term retention theme. Mass header/footer updates, mass approvals for mergers, rebrands, new policy imports, large-scale regulatory change. Practical customer value, not roadmap theater.

### Reporting
Mid-transition. Moving away from legacy patterns through SQL upgrades, new reporting framework, and Omni-related direction. Backup path has significant strain under large customers (timeout handling, incremental behavior, architecture limitations).

## Tech Stack

- **Legacy PHP monolith** with significant technical debt
- Moving from **CodeIgniter** toward **Symfony 7.2 / PHP 8.5** with **API Platform**
- **Doctrine ORM**
- **OnlyOffice** for document editing
- **Elasticsearch** (moving toward **OpenSearch**)
- **AWS** infrastructure - access and knowledge concentrated in a few people
- Supporting services: CloudFormation, Lambda, Terraform, S3, Redis, cron jobs
- **Notion** for engineering/QA docs, **Jira** (Cosmos project) for work intake, **Zendesk** for defects, **Pendo** for usage data

## Architecture Reality

The architecture is not just old - it's inconsistent. Deeply nested code, inconsistent rules, mixed patterns, brittle folder structures. Historical growth without sustained structural discipline. Zend-led Symfony migration is active but framework migration alone does not equal architectural maturity.

## Key People

### Leadership and Product
- **Glenn Orr** - CTO. Technically strong, repeatedly described as weak on process and operational clarity.
- **Lily He** - CPO. Roadmap and prioritization influence.
- **Ramona Jackson** - Product Manager for Policy. Main source of roadmap clarity, customer-facing prioritization. Strong signal source.
- **Jess Edwards** - VP of Client Experience. Key operational stakeholder across CX/training/support.

### Core Engineering
- **Paul Zorn** - Senior Software Cloud Architect. Practical linchpin, major bottleneck, single point of failure. Owns too much - architecture, pipelines, blockers, AWS, release/process gravity all pull toward him. Multiple sources describe strong dependency risk.
- **Ben Lamarita** - DevOps. Critical to AWS/platform operations and tenant onboarding. High leverage, high dependency.
- **Fred Woods** - Senior engineer for hard/core issues, Doctrine, backend/platform depth, StayAlert maintenance.
- **Avni Rexhepi** - Deep LMS/domain knowledge, long tenure, authored LMS.
- **Brian Sabat** - Deep PMAN legacy knowledge. High leverage on current-state system behavior.
- **Brian Moore** - Senior PHP contributor getting up to speed in PMAN.
- **Christian Valderrama, Joshua Martin, Muneeb Mohammed, Will Kirkhope** - engineering contributors across feature work, debugging, migration, operational fixes.

### QA
- **Devi Nallappan** - central QA backstop, manual-heavy, trusted quality gate.
- **Aaron Downing** - QA automation/Playwright/regression suite, but with reliability concerns.
- **Abe James** - manual QA, dependable in narrow scope, not growth-oriented toward automation.

## Current State

### What's Being Worked On
Zend-led Symfony modernization (PMAN V3), OnlyOffice upgrade, backup and reporting reliability, search optimization, mass actions, accessibility remediation, observability/monitoring, LDAP/SSO/infrastructure, release stabilization.

### What's Broken
- **Structural**: deep tech debt, inconsistent architecture, onboarding friction
- **Delivery**: error-prone releases, cadence being throttled, hotfixes/rollback are normal
- **Quality**: immature automated test coverage, Selenium/TestCafe migrating to Playwright, weak backend test seams
- **Operational**: backup headaches for large clients, report failures, weak observability
- **Product gaps**: weak search, incomplete bulk admin, narrow workflows, accessibility urgency, reporting mid-transition

### What Matters Most
1. Stability over feature vanity - Q1-Q2 capacity structurally constrained
2. Reducing dependency on Paul and other hero patterns - delivery risk, knowledge risk, burnout risk
3. Turning modernization into internal capability, not vendor theater

## Integration with Ntracts

MCN is part of the broader Ntracts portfolio under the Tract naming scheme. CLM Tract, Policy Tract, and Compliance Tract are distinct products for different market segments. 2026 goal: each product must win independently. CLM priority is differentiation. Policy and Compliance priorities are retention.

Integration is incomplete organizationally. Weak post-acquisition communication, insufficient intentional integration, limited cross-team visibility. Real technical intersections exist (Omni, Snowflake, accessibility, eventual brand/UI alignment) but the operating reality is still two partially integrated worlds.

Policy is not the growth engine right now. It must stop bleeding trust, retain customers, and modernize enough to become governable.
