
<!-- BACKLOG.MD MCP GUIDELINES START -->

<CRITICAL_INSTRUCTION>

## BACKLOG WORKFLOW INSTRUCTIONS

This project uses Backlog.md MCP for all task and project management activities.

**CRITICAL GUIDANCE**

- If your client supports MCP resources, read `backlog://workflow/overview` to understand when and how to use Backlog for this project.
- If your client only supports tools or the above request fails, call `backlog.get_backlog_instructions()` to load the tool-oriented overview. Use the `instruction` selector when you need `task-creation`, `task-execution`, or `task-finalization`.

- **First time working here?** Read the overview resource IMMEDIATELY to learn the workflow
- **Already familiar?** You should have the overview cached ("## Backlog.md Overview (MCP)")
- **When to read it**: BEFORE creating tasks, or when you're unsure whether to track work

These guides cover:
- Decision framework for when to create tasks
- Search-first workflow to avoid duplicates
- Links to detailed guides for task creation, execution, and finalization
- MCP tools reference

You MUST read the overview resource to understand the complete workflow. The information is NOT summarized here.

</CRITICAL_INSTRUCTION>

<!-- BACKLOG.MD MCP GUIDELINES END -->

# Project Agent Instructions

## Project Context

This repository is the durable product and delivery record for `agent_company`.
The product goal, intent, scope, and high-level technology boundaries are defined
in `.backlog/docs/intent/goal.md`. Operational constraints for agent decisions
are in `.backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md`.

The planned application is a monorepo with these application areas:

- `backend/`: Python 3.14 FastAPI Lambda backend using ports and adapters.
- `frontend/`: React TypeScript Vite SPA using Tailwind CSS and shadcn/ui.
- `infra/`: AWS SAM infrastructure and local integration support such as Mockoon.

Do not introduce a new top-level application directory, runtime, framework,
database, cloud service, authentication model, or deployment model without a new
user-approved ADR.

## Canonical Surfaces

- Backlog.md is the durable source for tasks, specs, ADRs, acceptance criteria,
  implementation plans, implementation notes, review evidence, deploy notes, and
  final summaries.
- After the project reset, `.backlog/decisions/` contains no accepted ADRs by
  default. Treat ADRs as canonical only when they exist and were explicitly
  approved by the user.
- ADRs are for user-approved high-level decisions. Agents must not create or
  accept detail-level ADRs unless the user explicitly requests that decision.
- Agent HOW-level decisions belong in Backlog specs, task plans, implementation
  notes, and final summaries inside the relevant task scope.
- Multica is the routing and handoff surface for agent assignments. Do not model
  agent workflow phases as Backlog.md tasks.
- Use Backlog.md MCP for `.backlog/docs`, tasks, and configuration. Use the
  Backlog.md CLI only when the MCP surface does not expose the required Backlog
  operation.
- Do not edit `.backlog` task or document Markdown by hand when an MCP or CLI
  operation exists for the change.

## Required Reading

Before planning or implementation, read the minimum relevant context:

- Project goal: `.backlog/docs/intent/goal.md`
- Agent constraints: `.backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md`
- Bounded context map: `.backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md`
- Accepted ADRs in `.backlog/decisions/*.md`, only if files exist
- Relevant Backlog task and linked specs or ADRs
- Existing code, tests, commands, and local conventions once application code
  exists

## Stop Rules

Stop and ask for a decision or record `Blocked` when a change would:

- conflict with the project goal, governance, a linked spec, or an accepted ADR
- add a new AWS service, library, runtime, top-level application directory, public
  API contract, authentication model, or production data source
- require production deploy, production data, credentials, secrets, cloud
  permissions, or external-service terms that are not documented
- lock a public API, DynamoDB key/index model, IAM scope, deploy model, Auth
  domain contract, or cross-context contract outside a relevant task or detail
  specification
- expose passwords, token plaintext, token digests, API keys, JWTs, PII, or raw
  external-service credentials in logs, events, API responses, fixtures, or docs
- require guessing a business rule, retention rule, legal/compliance rule,
  investment-advice boundary, or cross-context deletion policy

## Validation Defaults

Run the narrowest relevant checks for the touched area. If an area has no
configured commands yet, record that as a limitation instead of inventing a new
toolchain.

- Backend checks must cover domain/use case tests without AWS dependencies,
  Ruff, mypy, and adapter tests with mocks when relevant.
- Frontend checks must cover ESLint, unit tests, and Playwright for user-visible
  high-value flows when relevant.
- Infra checks must cover SAM template validation and least-privilege IAM review
  when infrastructure is touched.
- Every completed task must include validation evidence or an explicit reason the
  validation is not yet runnable.

## Definition of Done

A Backlog task is ready for completion only when:

- acceptance criteria have been verified against the implemented scope
- relevant checks have passed or the missing command/environment is documented
- secrets, tokens, credentials, and PII are not exposed
- public API, data, infrastructure, and operation contracts are updated when
  changed
- `Final Summary` records the outcome, validation, and remaining limitations
