# MyBatisCodeHelper-Pro

[![JetBrains Plugins](https://img.shields.io/jetbrains/plugin/v/9837-mybatiscodehelperpro.svg)](https://plugins.jetbrains.com/plugin/9837)
[![Downloads](https://img.shields.io/jetbrains/plugin/d/9837.svg?style=flat-square)](https://plugins.jetbrains.com/plugin/9837)

> **Spend less time on MyBatis rework and reduce unnecessary AI token usage.**

Spend less time finding XML, copying schemas, and repeating project conventions. MyBatisCodeHelper-Pro connects project context, code generation, and checking tools to your AI assistant to help reduce manual context gathering and repeated debugging.

**[Connect your AI assistant](/en/quickstart.md)** · **[Try / buy Marketplace Edition](https://plugins.jetbrains.com/plugin/14522-mybatiscodehelperpro-marketplace-edition-)** · [Features and Free / Pro comparison](/en/features.md)

## Where time and tokens can be saved

- Query mapper metadata and actual columns on demand, reducing manual context gathering.
- Read project generator profiles and generate repetitive code with tools, reducing repeated instructions and model output.
- Locate parameter and mapping issues with static checks, then inspect SQL for specific inputs to guide fixes.
- Generate mapper test scaffolding without starting Spring, then add inputs and assertions to verify results.

Lower token usage can reduce metered AI charges. With a fixed subscription, benefits mainly come from saved time and quota. Tool definitions, calls, and results also consume tokens, so savings depend on the task, model, and client. Compare total usage, elapsed time, manual corrections, and verification results for the same task and project starting point; do not treat an unmeasured percentage as a guaranteed saving.

## Start with a real task

Ask your AI assistant to add an optional filter to an existing mapper query:

1. Locate the mapper XML and inspect the existing statements.
2. Read the actual table columns and confirm parameter types.
3. Modify the interface and SQL using project conventions.
4. Validate the mapper and report executed and skipped checks.
5. Render SQL for representative inputs; run tests with meaningful assertions when checking business behavior.

[Follow the setup and task walkthrough](/en/quickstart.md).

## What the plugin contributes

| Task | Plugin capabilities | Details |
| --- | --- | --- |
| Understand an existing mapper | Interface / XML lookup and statement metadata | [MCP tools](/en/mcp.md) |
| Check AI edits | Parameter, mapping, reference, and static syntax checks | [Validation reference](/en/mcp.md) |
| Inspect dynamic SQL | Render for supplied inputs, check syntax, optionally execute against a test database | [SQL tools](/en/mcp.md) |
| Generate code in project style | Generator profile, CRUD and mapper test scaffolding | [Code generation](/en/databaseToCrud.md) |

Static validation only attests the checks that ran. Read skipped checks as well. Rendering SQL or generating a test skeleton does not establish business correctness.

## Teach the AI the workflow

Versions with **Generate MyBatis AI Skill (SKILL.md)** can generate project skills for Claude Code, CodeBuddy, and WorkBuddy, or a Cursor rule. These describe how to read context, use the tools, and validate changes. Configure the MCP connection separately and confirm the tools are visible in your client.

[Setup instructions](/en/quickstart.md) · [MCP reference](/en/mcp.md)

## Use it directly in IDEA

- [Completion and inspections](/en/complete.md), [refactoring](/en/refactor.md), and [ResultMap support](/en/resultMap.md).
- [Method name to SQL](/en/methodNameToSql.md), [SQL to mapper](/en/sqlToMybatis.md), and [JOIN generation](/en/join.md).
- [Database code generation](/en/databaseToCrud.md) and [templates](/en/generateByTemplate.md).

![Generate code from a database](https://images.brucege.com/databaseCrud.gif)

## Choose the edition for your purchase channel

For organizations and users outside China, use [Marketplace Edition](https://plugins.jetbrains.com/plugin/14522-mybatiscodehelperpro-marketplace-edition-). For licenses purchased on brucege.com, install the edition without Marketplace Edition in its name. Activation channels differ; trial, pricing, and licensing terms are shown by each purchase channel.

[Installation](/en/install.md) · [Full feature comparison and credits](/en/features.md) · [Release notes](/en/changelog.md)
