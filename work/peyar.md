[← Profile](../README.md)

# PEYAR
### Customer management for small businesses

<sub>Active development · Private source</sub>

PEYAR brings customer records, sales stages, activity history, and follow-ups into one workspace. The product centers on a practical workflow: understand the customer, see what happened last, and decide what needs to happen next.

## Product scope

- Maintain customer records and notes.
- Organize customers by sales stage.
- Create, review, and complete follow-ups.
- Keep activity history alongside the customer record.
- Work with individual team accounts and configurable access.

My work on PEYAR spans product direction and full-stack development, with particular attention to how daily workflows connect to the underlying data and access model.

## System design

| Layer | Approach |
| --- | --- |
| Application | TypeScript, React, and Next.js |
| Data | PostgreSQL with Prisma |
| Identity | Better Auth and database-backed sessions |
| Organization | A modular monolith with business-scoped workspaces |

The server resolves a workspace against the signed-in user's membership. Missing or inactive membership is rejected. Authorization then combines roles, permissions, and resource scopes.

This separates two questions: whether someone belongs to a business, and which actions or records they can access within it. Customer and follow-up scopes support assignment-based access; a reserved team scope is explicitly rejected until that hierarchy is implemented.

## Engineering decisions

**Keep the application cohesive.** A modular monolith keeps the initial product in one application while giving business concerns distinct boundaries.

**Check access on the server.** The workspace URL identifies the requested business; it does not establish permission to access it.

**Keep the scope focused.** Customer management and follow-ups form the core. Broader inbox and automation features remain outside this overview.

## Current status

The product is under active development. This overview describes its implementation and design; it does not claim customer adoption, revenue, or independently audited security. The source remains private.

<sub>Overview updated October 5, 2026.</sub>
