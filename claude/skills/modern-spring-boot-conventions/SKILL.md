---
name: modern-spring-boot-conventions
description: "Automatically enforces modern Spring Boot 3.x+ microservice conventions: strict constructor injection, record-based ConfigurationProperties, strict placeholder discipline without default fallback values (.env.example discipline), RFC 7807 ProblemDetail, RestClient, JdbcClient, and Testcontainers @ServiceConnection."
---

# Modern Spring Boot Guardrails & Skill Router

Entry point for this plugin's guardrails in Claude Code. Before acting, read the full standard:

`${CLAUDE_PLUGIN_ROOT}/rules/modern-spring-boot-conventions.md`

It routes each kind of task to the specialized skill of this plugin and lists the non-negotiable rules.
In Claude Code those skills are namespaced: invoke `modern-spring-boot-best-practices:<skill-name>`.

> Generated from `rules/modern-spring-boot-conventions.md`, which is also the Antigravity rule. Edit the rule, not this file.
