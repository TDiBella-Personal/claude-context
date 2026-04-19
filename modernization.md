# Policy Manager Modernization (V3)

## What This Project Is

Migration of Policy Manager from a legacy CodeIgniter 3 / older PHP codebase to Symfony 7.2 / PHP 8.5. The goal is to preserve existing business behavior while replacing a codebase with poor maintainability, no automated tests, no observability, no structured error handling, and a PHP version approaching end-of-life.

This is a modernization-and-transition program, not just a code rewrite. Delivery success depends equally on rollout design, rollback safety, environment readiness, cron behavior, reporting transition, customer communication, team retraining, and explicit ownership.

## Delivery Path

**Zend is the active vendor delivery path.** Glenn stated on March 18, 2026 that David reviewed Plan B (internal alternative, PMANV3_i5) and judged the risk too high. Plan B is dead.

### Zend Progress (as of March 6, 2026)
- 4-month project described as halfway complete, slightly ahead of schedule
- Component progress: ~30% traits, ~70% libraries, ~55% controllers, ~75% models, ~5% views (Twig base structure done)
- Authentication targeted for completion by mid-March
- Concrete commit activity in SSO/auth, backend refactoring, entity/repository migration, approval and document service cleanup, test additions
- Key contributors: rsalvatori (backend/auth/refactor/tests), Valdir Bruxel Jr (AssignCompetencies controller/template)

### Delivery Concerns
- Gap between percentage-complete reporting and runnable end-to-end proof
- SOW uses commercially reasonable efforts over ~4 months, not milestone-based acceptance
- No validated feature parity baseline exists in project materials

## Architecture - Before and After

### Before
- CodeIgniter 3 on older PHP (~7.4-era)
- 1,116 PHP files, zero automated tests, zero observability
- No structured error handling, very large god classes
- Structurally inconsistent with accumulated organizational drift

### After (Target)
- Symfony 7.2 / PHP 8.5
- Domain-Driven Design modular monolith with 14 bounded contexts
- Strict layering: Domain, Application, Infrastructure, Presentation
- CQRS commands and handlers, domain events
- Doctrine ORM 3.x, Twig presentation
- Structured logging, Prometheus metrics, distributed tracing
- Security hardening, containerized runtime
- Strangler-fig deployment with shared database compatibility and instant rollback through routing reversal

## Key Decisions

- **Proceed with Zend** - Plan B terminated after David's risk assessment (March 18, 2026)
- **Rollout must be reversible** - phased rollout, smaller clients first, DNS flipping, V2/V3 share same database with no schema changes enabling rollback
- **Code delivery is not production readiness** - infrastructure, testing, client readiness are separate post-delivery workstreams
- **Reporting and data work are explicit workstreams** - Omni, Snowflake, cron jobs each have separate ownership and planning
- **Cron jobs are a major risk area** - dedicated stories, fallback to V2 cron jobs if needed, explicit monitoring for slippage
- **Team training is mandatory** - PHP/Symfony training, repo review, knowledge checks required
- **Early customer communication** - especially for reporting access changes where non-admin users may lose access in V3

## Timeline and Milestones

- **Zend paid through May 5, 2026** - major executive target and commercial boundary, with 4-week warranty after
- **May 5 is vendor delivery, not go-live** - Ramona was explicit about this distinction
- **Cron job completion** - push toward end of May, broader schedule allows 3-month window
- **Targeted regression** - starting May
- **Larger coordinated testing** - before end of June
- **VPN decommissioning** - end of June, affects ~40 clients
- **V2 sunset** - potentially September, unless cron/batch fallback needs keep it alive longer

### Rollout Concept
1. Move smaller clients to V3 first
2. Verify stability
3. Flip remaining clients overnight using DNS
4. Preserve rollback to V2 (no DB schema changes required)

## Risks

- **Evidence gap** - progress reporting doesn't prove runnable end-to-end readiness
- **Timeline** - aggressive schedule with weak governance leverage (time-based billing, not milestone acceptance)
- **Operational readiness** - environment prep, QA capacity, production-like data, regression planning, client transition, cron behavior, VPN transition, proxy setup all remain open
- **Cron jobs** - one of the biggest risks; V2 fallback exists but is not the preferred end state
- **Reporting parity** - admins expected to have parity, non-admin users may lose access
- **Vendor dependence** - Zend completion does not equal internal readiness or long-term ownership
- **SETA FPDF licensing** - compatibility with newer PHP still open

## Blockers

- Fivetran/proxy setup delayed by technical issues
- Environment and QA readiness incomplete (who tests, where, with what data)

## Open Questions

- What is the exact validated feature parity baseline?
- What post-delivery criteria formally define go/no-go?
- How much of Plan B material can Zend reuse? (Glenn planned to share with Adam - no follow-up captured)
- What is the final internal ownership model after launch?

## Key People (Project-Specific Roles)

### Internal
- **Tom** - engineering leadership and program oversight. QA capacity planning, rollout questions, beta testing, ownership allocation, reporting transition, training.
- **Lily He** - program and execution oversight. QA capacity, ownership assignment, reporting communication, customer impact, cron risk monitoring, go/no-go visibility.
- **Paul Zorn** - technical lead across cron jobs, infrastructure, PDF/licensing, Snowflake guidance, rollout/rollback design, training. Repeatedly central to architecture and transition decisions.
- **Ramona Jackson** - execution and planning lead. Cron jobs, Omni/Snowflake visibility, regression strategy, environment/data prep, customer communication.
- **Brian (Sabat)** - contributor in rollout, cron, training. Suggested pair programming for cron job tickets.
- **Glenn Orr** - executive/technical sponsor. Evaluated Zend vs Plan B, communicated with board, analyzed Zend code activity.
- **David Paschall** - decision-maker on Zend vs Plan B (March 18).
- **Tanner** - VPN transition work (~40 clients affected).
- **Avni Rexhepi** - proposed owner for Snowflake work (database experience).
- **Brian Sabat** - proposed point person for cron jobs.
- **Eddie Wuerch, Ajay Pratap Meena** - needed for Omni reporting knowledge transfer.

### Vendor (Zend)
- **Adam** - Zend lead/primary delivery representative in status meetings.
- **rsalvatori** - primary backend/auth/refactor/test contributor.
- **Valdir Bruxel Jr** - AssignCompetencies controller/template work.

## Dependencies

### Technical
- PHP 7.4-era to 8.5 runtime upgrade
- CodeIgniter 3 to Symfony 7.2 / Smarty to Twig
- Shared MySQL database compatibility (no schema divergence for rollback)
- Cron job migration and validation
- Omni reporting transition and customer-built report migration
- Snowflake views and data work
- Environment/infrastructure readiness (EC2, proxy, health checks)
- SETA FPDF licensing for PDF under modern PHP

### Organizational
- QA capacity, test planning, prod-like data
- CX participation in validation and customer communication
- Engineering training on PHP/Symfony patterns
- Explicit ownership assignment across all workstreams (still being actively clarified as of late March)
