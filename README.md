# Awesome-Database-Schema-Migration

# Top Database Schema Migration Platforms Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**
*Focused on Schema Migration, Declarative Schema-as-Code, Version Control & Database CI/CD*
**Last updated: October 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Database Schema Migration**. These tools help developers and DBAs manage schema changes with version control, automate deployments, and integrate database changes into CI/CD pipelines.

**Examples** include Liquibase, Flyway, Atlas, Bytebase, Sqitch, Prisma Migrate, dbmate, Alembic, Goose, and golang-migrate (the category leaders).

**Open-source emphasis**: Database schema migration has a **mature and production-proven open-source ecosystem**. **Flyway** and **Liquibase** dominate imperative migrations—Flyway for SQL-first simplicity and Liquibase for cross-database abstraction with explicit rollbacks . **Atlas** has emerged as the de facto standard for **declarative schema-as-code**, bringing Terraform-like workflows and safety analyzers to database migrations . **Bytebase** is the only database CI/CD project in the CNCF Landscape, providing web-based review workflows and 200+ SQL lint rules . **golang-migrate** leads in GitHub stars (18,919) for simple, database-agnostic migrations . This section documents these production-grade solutions.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents

- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Liquibase Secure](https://www.liquibase.com/)**
  Commercial edition of Liquibase (formerly Datical DB). Adds **policy checks** (dangerous pattern blocking), structured rollbacks, governance, and regulatory compliance mapping (SOX, PCI DSS, DORA). Sold in Starter, Growth, Business, and Enterprise tiers, each priced by quote and bounded by application and database type coverage. **License note**: Liquibase Community 5.0 moved from Apache 2.0 to the **Functional Source License 1.1** in September 2025, which has triggered license-policy reviews at organizations including Keycloak (CNCF does not permit source-available licenses) .

- **[Flyway Enterprise](https://www.red-gate.com/products/flyway/enterprise/)**
  Commercial edition of Flyway (acquired by Redgate in 2024). Adds **Undo script generation** for rollbacks, **drift detection**, **object-level versioning**, and **custom code analysis** for SQL Server, PostgreSQL, Oracle, and MySQL . Over **200,000+ people** use Redgate's database DevOps tools.

- **[Bytebase Cloud](https://bytebase.com/)**
  Managed version of the open-source Bytebase platform. Provides database CI/CD with approval workflows, SQL review, data masking, and audit logging. **Community edition**: Free forever for up to 20 users and 10 database instances; **Pro**: $20/user/month with SSO, user groups, and a 7-day audit log; **Enterprise**: custom pricing with data masking, JIT access, and unlimited audit retention .

## Open-Source GitHub Projects

### Imperative Migration Frameworks

- **[Flyway](https://github.com/flyway/flyway)**
  **The developer-friendly SQL-first migration tool.** **Apache-2.0 licensed** (Community edition), Java-based. Uses **versioned SQL scripts** (`V{version}__{description}.sql`) applied in order, tracked by a `flyway_schema_history` table. **Key features**: **50+ database support**; Spring Boot integration with single property update; baseline for introducing Flyway to existing databases . **Target audience**: Developer-first teams wanting minimal setup. **Tradeoff**: Automatic rollback and schema diff are commercial features; no declarative mode .

- **[Liquibase](https://github.com/liquibase/liquibase)**
  **The cross-database abstraction tool.** **Functional Source License 1.1** (Community 5.0+), converting to Apache 2.0 after two years. Uses a **changelog** concept with **changesets** written in SQL, XML, YAML, or JSON. **Key features**: Database-agnostic changelogs supporting **60+ databases**; **standardized rollbacks** (first-class OSS feature); preconditions, tagging, and drift detection . **Target audience**: Enterprise and regulated environments needing governance. **Tradeoff**: XML/YAML format is verbose; abstraction can generate suboptimal SQL .

- **[Sqitch](https://github.com/sqitchers/sqitch)**
  **The dependency-graph-based migration tool.** Created by David Wheeler in 2012. **Model**: Each change has a name; dependencies are explicit in `sqitch.plan`. **Key features**: **Dependency resolution** (no version-number collisions); **verify is first-class**; **DB-neutral** (Postgres, MySQL, Oracle, SQLite, Snowflake, Firebird, Vertica, Exasol). **Target audience**: Monolith DBs with 1000+ migrations. **Tradeoff**: Learning curve; smaller community; CLI-only; Perl dependency .

### Declarative Schema-as-Code

- **[Atlas](https://github.com/ariga/atlas)**
  **The de facto standard for declarative schema-as-code.** **Apache-2.0 licensed** (Community edition), Go-based. **Two modes**: **Declarative** (`atlas schema apply` — diff and apply directly) and **Versioned** (`atlas migrate diff` — write diff as SQL file, apply later; recommended for production). **Key features**: **Schema as Code** (HCL, SQL, or ORM); **50+ safety analyzers** detecting destructive changes, data-dependent modifications, and table locks; **Security-as-Code** for roles and permissions; **cloud-native CI/CD** (Kubernetes operator, Terraform provider, GitHub Actions, GitLab CI) . **Target audience**: Teams comfortable with IaC like Terraform; multi-DB environments. **Tradeoff**: Declarative model may handle column rename as drop+add; gap between free and paid is large .

- **[SchemaHero](https://github.com/schemahero/schemahero)**
  **Kubernetes operator for declarative database schema management.** **Apache-2.0 licensed**, Go-based. **Key concept**: Database table schemas are expressed as **Kubernetes resources** deployed to the cluster; SchemaHero calculates the required `ALTER TABLE` statement and applies it. Manages databases deployed in the cluster or external (RDS, Google CloudSQL). **Target audience**: Kubernetes-native teams wanting GitOps for database schemas .

### Database DevOps Platforms

- **[Bytebase](https://github.com/bytebase/bytebase)**
  **The only database CI/CD project in the CNCF Landscape.** **Apache-2.0 licensed**, Go and TypeScript-based. **Web-based collaboration workspace** for DBAs and developers — "GitLab/GitHub for DBs" . **Key features**: **GitOps integration** for database-as-code workflows; **200+ SQL lint rules**; **approval workflows** with DBA review; **staged auto-deploy** (dev → staging → prod); **schema drift detection** with alerts; **data masking** and **access control** . **Supported databases**: 50+ including PostgreSQL, MySQL, MongoDB, Redis, Snowflake, Oracle, SQL Server. **Community edition**: Free for up to 20 users and 10 instances; Pro $20/user/month . **Target audience**: Teams needing a platform with governance and audit trails.

- **[grate](https://github.com/erikbra/grate)**
  **Automated database deployment using plain old .sql scripts.** **Open-source**, Docker image available. Supports **SQL Server, MySQL/MariaDB, PostgreSQL, and SQLite**. **Key philosophy**: "We don't believe in writing database migrations in C#." Write scripts at dev time alongside feature code. **Use your whole DBMS** — table-valued parameters, data compression, fancy indexes, replication, fine-grained permissions. **Target audience**: Teams wanting plain SQL scripts with version alignment to application releases.

### ORM-Integrated Migrations

- **[Prisma Migrate](https://github.com/prisma/prisma)**
  **Hybrid declarative/imperative migration tool integrated with Prisma ORM.** **Apache-2.0 licensed**, TypeScript-based. **How it works**: Data model described declaratively in Prisma schema; Prisma generates SQL migration files; generated SQL is fully customizable. **Key features**: Migration history of `.sql` files; shadow database for development; works in development and production. **Note**: For MongoDB, use `db push` instead of `migrate dev` . **Target audience**: Teams already using Prisma ORM.

- **[Alembic](https://github.com/sqlalchemy/alembic)**
  **Python/SQLAlchemy migration tool.** **MIT licensed**. **Key features**: Autogenerate from model diffs; branching and merge support; downgrade scripts for rollbacks . **Target audience**: Python/SQLAlchemy teams. **Note**: Autogenerate may miss custom types and triggers — always review generated migrations .

- **[Goose](https://github.com/pressly/goose)**
  **Go database migration tool.** **Open-source**. Supports **SQL files and Go migrations**. **Key features**: Simple up/down migrations; database-agnostic; CLI and library usage . **Target audience**: Go applications needing lightweight embedded migrations.

- **[golang-migrate](https://github.com/golang-migrate/migrate)**
  **The most starred open-source migration tool (18,919 GitHub stars).** **Open-source**, Go-based. **Key features**: SQL files up/down; database-agnostic; simple CLI and library usage . **Target audience**: Go teams wanting simple, battle-tested migrations.

### Additional Strong Open-Source Options

- **Imperative Migration**: **Flyway** (SQL-first, 50+ DBs), **Liquibase** (cross-DB abstraction, explicit rollbacks), **Sqitch** (dependency graph, verify first-class) .
- **Declarative Schema**: **Atlas** (HCL/SQL/ORM, 50+ analyzers), **SchemaHero** (Kubernetes operator) .
- **DevOps Platforms**: **Bytebase** (CNCF, web GUI, approval workflows, 200+ lint rules) .
- **Script-Based**: **grate** (.sql scripts, version alignment) .
- **ORM-Integrated**: **Prisma Migrate** (TypeScript, hybrid), **Alembic** (Python/SQLAlchemy), **Goose** (Go) .
- **Language-Specific**: **golang-migrate** (18,919 GitHub stars) , **Drizzle Kit** (13,644,360 npm downloads/week) .

**Frameworks for building custom systems**: Combine **Flyway** for simple SQL-first migrations, **Liquibase** for database-agnostic changelogs with rollback support, **Atlas** for declarative Terraform-style schema management with linting and Security-as-Code, **Bytebase** for team collaboration with approval workflows and audit trails, and **Skeema** for MySQL declarative GitOps. Add **PostgreSQL** for metadata persistence and **Docker** for deployment.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Database schema migration platforms handle sensitive production schemas and data; ensure proper access controls and compliance with change management policies.
- **Open-source reality**: The open-source ecosystem for database schema migration is **mature and production-proven**. **Flyway** and **Liquibase** remain the two dominant imperative tools, each with broad database support and active communities . **Atlas** has emerged as the de facto standard for declarative schema-as-code, with 50+ safety analyzers and Security-as-Code . **Bytebase** is the only database CI/CD project in the CNCF Landscape, providing web-based governance . **golang-migrate** leads in GitHub stars (18,919) for simple, database-agnostic migrations . However, **commercial editions** (Flyway Enterprise, Liquibase Secure) provide **regulatory compliance mapping, structured rollbacks, and enterprise support** that open-source editions require additional tooling to match. **License note**: Liquibase Community 5.0 moved from Apache 2.0 to the **Functional Source License 1.1** in September 2025, which has triggered license-policy reviews at organizations including Keycloak (CNCF does not permit source-available licenses) . The open-source path is **genuinely viable** for most teams, with the choice driven by workflow preference (SQL-first vs. changelog vs. declarative vs. dependency-graph) and governance requirements.

---

**Made for database engineers, DevOps teams, DBAs, and platform engineers.**
Let's make database schema migration more open, transparent, and reliable.
