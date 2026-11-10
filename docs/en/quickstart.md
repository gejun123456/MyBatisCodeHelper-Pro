# Quick start: edit and validate a mapper with AI

Use an existing MyBatis project and a development / test database. Keep the project open in IntelliJ IDEA and wait for indexing to finish.

## 1. Install the correct edition

For organizations and users outside China, install [MyBatisCodeHelperPro (Marketplace Edition)](https://plugins.jetbrains.com/plugin/14522-mybatiscodehelperpro-marketplace-edition-) from **Settings / Preferences → Plugins → Marketplace**. Follow the Marketplace instructions for the trial and activation.

Licenses purchased on brucege.com apply to the edition without Marketplace Edition in its name. Purchase and activation channels differ. See [installation](/en/install.md) and use the compatibility range shown on the relevant Marketplace page.

## 2. Configure a database

Connect the project's development / test database in IDEA's Database tool window. Confirm that the required tables and columns are visible, and identify the target data source and schema when more than one is configured.

See [database configuration](/en/configure.md). Without an available data source, some static checks still work, but skipped schema checks must be reported.

## 3. Connect your AI client

In IDEA, choose **Tools → MyBatisCodeHelper → Start MyBatis MCP Server**. The startup dialog shows the actual service URL and client configuration instructions. The default endpoint is `http://127.0.0.1:63340/mcp`.

Use the configuration method supported by your client. The dialog can generate a project `.mcp.json` for clients that support it; other clients use different locations. Versions with WorkBuddy integration can write the server configuration using the dialog's WorkBuddy button.

Confirm in your AI client that the `mybatis` service is connected and tools such as `find_mapper_xml` and `validate_mybatis_mapper` are visible. Creating a configuration file alone does not establish a connection. See the [MCP reference](/en/mcp.md).

## 4. Generate an AI skill or rule

Versions with this feature provide **Tools → MyBatisCodeHelper → Generate MyBatis AI Skill (SKILL.md)**, also available from the MCP dialog or settings page.

| Client | Project file |
| --- | --- |
| Claude Code | `.claude/skills/mybatis-code-helper/SKILL.md` |
| CodeBuddy | `.codebuddy/skills/mybatis-code-helper/SKILL.md` |
| WorkBuddy | `.workbuddy/skills/mybatis-code-helper/SKILL.md` |
| Cursor | `.cursor/rules/mybatis-code-helper.mdc` |

Select your client, review the preview, and generate. An existing skill / rule at the same path is overwritten. Reload the project or client as prompted. MCP connection and skill loading are separate steps.

If the menu is missing, check your installed version's release notes. You can still use the task prompt below.

## 5. Try an actual task

Replace the mapper name and requirement with ones from your project:

```text
Use the mybatis MCP tools to add an optional status filter to the existing
list query in com.example.mapper.UserMapper.

1. Find its XML and inspect existing statements and actual table columns.
2. Confirm the status type and mapping. Follow the project's conventions;
   preserve return values and ordering, and avoid unrelated changes.
3. Validate the mapper, fix reported issues, and list checksSkipped.
4. Render SQL with execute=false for a missing status, a valid status,
   and a value with no matching rows. Inspect parameter and branch behavior.
5. Use a confirmed development / test database if execution is needed.
   If generating a test, review the connection and transaction settings,
   add valid inputs, fixtures, and result assertions before running it.
6. Report changed files, checks performed, actual test outcomes, and anything
   not verified. Do not equate generated tests or static checks with
   verified business behavior.
```

## 6. Review the evidence

Expect a concrete diff, actual schema information, executed and skipped static checks, and rendered SQL for the supplied inputs. If tests ran, review their execution results and assertions.

`execute=false` renders and checks SQL without database execution. `dryRun` requests a DML rollback after execution; rollback is not an isolation boundary. Use a development / test database for execution.

Generated tests are scaffolding with placeholder inputs and no business assertions, and setup may auto-commit writes. Review these settings before running.

## Troubleshooting

| Symptom | Check |
| --- | --- |
| No tools in the AI client | Server status, actual URL / port, and client enablement |
| Mapper or XML not found | Project indexing, namespace, module dependencies, and resource directories |
| Missing columns or skipped schema checks | Data source visibility, selected schema, and [configuration](/en/configure.md) |
| License validation failure | Trial / activation status and installed edition |

[MCP tools and configuration](/en/mcp.md) · [Features and editions](/en/features.md) · [Try / buy](https://plugins.jetbrains.com/plugin/14522-mybatiscodehelperpro-marketplace-edition-)
