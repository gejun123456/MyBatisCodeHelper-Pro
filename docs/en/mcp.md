# MyBatis MCP (Model Context Protocol) Support

MyBatisCodeHelper-Pro provides **MCP (Model Context Protocol)** support, enabling AI coding assistants (such as Claude Code) to interact directly with your MyBatis project, making MyBatis development faster, more accurate, and more context-efficient.

---

# 🚀 Why Use MyBatis MCP?

When working with MyBatis projects, AI coding assistants frequently need to:

* Locate the XML file corresponding to a mapper interface
* Inspect database table schemas
* Discover existing SQL statements

Without MCP, the AI typically searches the project, opens XML files, and extracts the required information itself. Besides consuming additional tokens, this also fills the conversation context with large amounts of XML that are irrelevant to the final answer.

## With MCP vs. Without MCP

| Operation                            | Without MCP                                               | With MCP                                  |                  Typical Savings                  |
| ------------------------------------ | --------------------------------------------------------- | ----------------------------------------- | :-----------------------------------------------: |
| Find mapper → XML mapping            | Search project files and verify mapping (~150–250 tokens) | **Single MCP call (~30–60 tokens)**       |                **~100–200 tokens**                |
| List SQL statements                  | Read XML file (~1,000–2,500 tokens depending on size)     | **Returns structured statement metadata** |              **~1,000–2,500 tokens**              |
| Query table columns                  | Read DDL or inspect database (~300–500 tokens)            | **Single MCP call (~50 tokens)**          |                **~250–450 tokens**                |
| Validate Mapper syntax & contracts   | Reading large XML manually invites hallucinations & misses| **Deep static analysis, ms-level diagnostics**| **Prevents dynamic SQL runtime bugs**          |
| Dynamic SQL simulation & safe execution | Manually write tests, start Spring, or guess branches  | **Branch evaluation, parameter mocking & DryRun** | **Instant verification without test containers** |
| Typical MyBatis development workflow | Multiple searches, XML reads, schema lookups              | **Direct MCP queries**                    | **Typically 60–90% less MyBatis-related context** |
> Locating a mapper XML saves only a small number of tokens. The larger savings come from avoiding large XML reads and schema lookups. During real development these operations are often combined, so the overall savings accumulate quickly.

---

# 📉 Cleaner Conversation Context

Without MCP, AI assistants often need to load entire XML files into the current conversation context.

For example, if a conversation involves three different mappers:

```text
Without MCP:
3 × ~2,000 tokens
≈ 6,000 tokens of XML occupying the current conversation context

With MCP:
3 × ~50 tokens
≈ 150 tokens of structured metadata
```

That's roughly **5,800 fewer tokens** occupying the context window.

A cleaner context allows the model to focus on the information that actually matters instead of large XML documents, often resulting in faster and more accurate responses.

---

# 📈 Larger Projects Benefit Even More

| Project Size | Typical XML Size |     XML Read Cost    | Working with 5 Mappers |
| ------------ | :--------------: | :------------------: | :--------------------: |
| Small        |      5–10 KB     |  ~1,000–2,500 tokens |  ~5,000–12,500 tokens  |
| Medium       |     15–30 KB     |  ~4,000–7,500 tokens |  ~20,000–37,500 tokens |
| Large        |     30–50 KB     | ~7,500–12,500 tokens |  ~37,500–62,500 tokens |

As projects grow, mapper XML files become larger and more numerous. MCP continues to return only the information the AI actually needs, making its advantages increasingly significant.

---

# 🛠️ Available MCP Tools

## `find_mapper_xml`

Find the XML file corresponding to a Java mapper interface.

**Input**

* Fully qualified mapper class name
* `.java` file path

**Output**

* Matching mapper XML file path(s)

```text
Input:
com.example.mapper.UserMapper

Output:
src/main/resources/mapper/UserMapper.xml
```

> Large projects often contain multiple XML files with identical names under different directories (for example, `mapper/` and `easycode/`). IDE-based indexing allows MCP to locate the correct mapping much more reliably than file searching alone.

---

## `find_mapper_interface`

Find the Java mapper interface corresponding to an XML file.

**Input**

* XML file path

**Output**

* Namespace
* Java interface path

```text
Input:
src/main/resources/mapper/UserMapper.xml

Output:
com.example.mapper.UserMapper
```

---

## `get_table_columns`

Retrieve database table columns.

**Input**

* Table name

**Output**

* Column names
* Corresponding Java types

```text
user

id          → Long
username    → String
email       → String
create_time → Date
```

> The AI can retrieve table metadata directly through MCP without manually opening a database client or inspecting DDL.

---

## `list_mapper_statements`

List SQL statements defined in a mapper.

**Input**

* Mapper interface (FQN or `.java` path)
* XML file path

**Output**

* Statement ID
* Statement type
* Line number

```text
selectByPrimaryKey   → select (line 28)
insert               → insert (line 40)
updateByPrimaryKey   → update (line 145)
deleteByPrimaryKey   → delete (line 35)
```

> Quickly discover available SQL statements without reading hundreds of lines of XML.

---

## `list_data_sources`

List project data sources.

**Output**

* Data source name
* Database type
* JDBC URL

---

## `generate_crud`

Generate MyBatis CRUD code for a database table.

**Input**

* `table` (required): database table name
* `projectPath`: absolute project path; optional when only one project is open
* `dataSource`: optional data-source selector, useful when multiple data sources are configured
* `modelName`: optional entity class name; defaults to the project's naming rule
* `referenceMapperXml`: optional existing mapper XML; reuses its XML / mapper layout
* `modelPackage` / `modelSrcRoot`: optional entity package and source root
* `mapperPackage` / `mapperSrcRoot`: optional mapper interface package and source root
* `xmlPackage` / `xmlSrcRoot`: optional mapper XML path and resources root
* `servicePackage` / `serviceSrcRoot`: optional Service implementation package and source root
* `serviceInterfacePackage` / `serviceInterfaceSrcRoot`: optional Service interface package and source root
* `generateService` / `generateServiceInterface`: optional Service generation switches
* `insertMethod`, `insertSelective`, `selectByPrimaryKey`, `updateByPrimaryKey`, `updateByPrimaryKeySelective`, `deleteByPrimaryKey`: optional CRUD method switches
* `batchInsert`, `updateBatch`, `updateBatchSelective`: optional batch method switches
* `useLombok`, `lombokGetterSetter`, `lombokBuilder`, `lombokAllArgs`, `lombokNoArgs`: optional Lombok switches
* `useCommonMapper`, `mapperAnnotation`, `mybatisFlex`, `addSchemaName`, `generateComment`, `useSwagger`, `noJdbcType`: optional framework and annotation switches
* `useMybatisPlus`, `mybatisPlusIdType`, `mybatisPlusStaticField`, `mybatisPlusGenerateByPrimaryKey`, `mybatisPlusGenerateUpdateAndInsertSelective`: optional MyBatis-Plus 3 switches

**Output**

* `status`
* `table`
* `modelName`
* `generatedFiles`
* `warnings`
* resolved `modelPackage`
* resolved `mapperPackage`
* resolved `xmlPackage`

> This is a write tool. It generates the entity, mapper interface, mapper XML, and optionally Service / Service Interface files. Location resolution uses explicit arguments first, then `referenceMapperXml`, then the project profile / module defaults. Style switches fall back to the current project profile when omitted.

---

## `generate_mapper_testcase`

Generate or update a MyBatis mapper testcase.

**Input**

* `mapper` (required): mapper interface FQN or `.java` path
* `projectPath`: absolute project path; optional when only one project is open
* `methodName`: optional mapper method name; when omitted, only the test class, mapper field and setup method are generated
* `dataSource`: optional test data-source selector
* `testPackage`: optional package for the generated test class; defaults to the mapper package
* `testFramework`: optional test framework, `JUNIT4` or `JUNIT5`

**Output**

* `status`
* `testClassName`
* `testClassPath`
* `configurationPath`
* `generatedFiles`
* `warnings`

> The tool creates or updates the mapper test class, the `setUpMybatisDatabase` method, the mapper field, and the `mybatisTestConfiguration` XML when needed. When `methodName` is provided, it also generates the corresponding test method; if that method already exists, the response includes a warning.

---

## `validate_mybatis_mapper`

Performs comprehensive static contract validation for MyBatis Mapper XML files and their corresponding Java interfaces using IntelliJ IDEA's deep inspection framework (DOM validation, MyBatis ParamLanguage, and OGNL test-expression checks). Detects discrepancies and defects before code is executed or committed.

**Validation Scope:**

* **XML Structure & Syntax**: Valid root element, tag closures, and formatting
* **DOM Mapping Contracts**: `resultType` resolution, `resultMap` property existence in entity POJOs, `association`/`collection` nested mappings
* **Parameter Binding**: `#{...}` placeholder consistency with Java interface `@Param` annotations or POJO properties
* **OGNL Test Expressions**: Variable references and syntax correctness in `<if test="...">` and `<when test="...">`
* **SQL Fragment References**: `<include refid="...">` existence (both local and cross-namespace)
* **Java-XML Coherence**: Namespace matching, interface method to XML statement ID pairing
* **Static SQL Grammar**: IntelliJ SQL dialect parser checks for statically rendered SQL
* **Database Schema Resolution (when IDE data source is configured)**: Validates table/column existence and `jdbcType` vs. physical DB column type compatibility

> **Coverage Contract**:  
> Statements containing dynamic tags (`<if>`, `<choose>`, `<foreach>`) cannot have every branch combination proven by static analysis alone. The tool provides a transparent `checksExecuted` / `checksSkipped` contract and gives targeted recommendations (`STATIC_CHECKS_PASSED_WITH_DYNAMIC_SQL`, etc.) guiding developers and AI to verify branches using `run_mybatis_sql` or testcases.

**Input**

* `mapper`: Mapper interface FQN (e.g. `com.example.mapper.UserMapper`) or `.java` path (use this or `xmlPath`)
* `xmlPath`: Mapper XML file path (use this or `mapper`)
* `statementId`: Optional. Validate a specific Statement ID; if omitted, all statements and resultMaps in the mapper are validated
* `projectPath`: Optional. Project root path

**Output**

* `valid`: Boolean. `true` if no blocking errors are found
* `recommendation`: Actionable recommendation, such as `ALL_STATIC_PASSED`, `STATIC_CHECKS_PASSED_WITH_DYNAMIC_SQL`, `PASSED_WITH_WARNINGS`, or `ERRORS_FOUND`
* `summary`: Contains `totalStatements`, `staticStatements`, `dynamicStatements`, `totalErrors`, `totalWarnings`, plus `checksExecuted` and `checksSkipped`
* `statements`: Per-statement analysis including dynamic tags list, `sqlAnalysisNotice`, errors, and warnings
* `resultMaps`: ResultMap mapping and property validation details
* `globalErrors` / `globalWarnings`: File-level diagnostics

---

## `run_mybatis_sql`

Renders and optionally executes MyBatis dynamic SQL with zero overhead—**without starting Spring Boot or writing test scaffolding**!

Supports dynamic branch evaluation (`<if>`, `<choose>`, `<where>`, `<trim>`, `<foreach>`, OGNL expressions), parameter injection, Druid AST syntax parsing, and safe database execution (with automatic DML transaction rollback `dryRun`, result set preview, and row limits).

**Input**

* **Statement Locator (choose one):**
  * `xmlPath` + `statementId` (or `methodName`): Locate via XML file and statement ID
  * `mapper` + `methodName` (or `statementId`): Locate via Java interface and method name
  * `rawXml`: Direct XML statement snippet (e.g. `<select id="find">SELECT * FROM user WHERE id = #{id}</select>`), allowing AI to validate newly generated XML snippets before saving to disk
* **Parameter Simulation & Branch Control:**
  * `params`: Key-value pairs for parameter values (JSON object, e.g. `{"id": 1, "status": "ACTIVE"}`)
  * `ifTests`: Explicit boolean overrides for `<if test="...">` conditions (e.g. `{"status != null": true}`)
  * `allIfTestsTrue`: Force all dynamic `<if test>` conditions to `true`
  * `allIfTestsFalse`: Force all dynamic `<if test>` conditions to `false`
* **Execution & Dialect Settings:**
  * `format`: Format and indent rendered SQL (default `true`)
  * `checkSyntax`: Validate rendered SQL syntax using Druid parser (default `true`)
  * `execute`: Execute rendered SQL against project database (default `false`)
  * `dryRun`: Roll back DML (insert/update/delete) immediately after execution (default `true`, preventing data modification)
  * `dataSource`: Target datasource name (defaults to configured project datasource)
  * `maxRows`: Max rows returned for queries (default 50)
  * `dbType`: SQL dialect: `mysql`, `postgresql`, `oracle`, `sqlserver`, `h2` (default auto-detected)
  * `username` / `password`: Optional database credential overrides
  * `projectPath`: Optional project root path

**Output**

* `status`: `success` or `error`
* `statementId`: Statement ID
* `statementType`: `select`, `insert`, `update`, `delete`
* `renderedSql`: Fully evaluated and rendered SQL string
* `parameters`: Parameter details (tokens, property names, used values, provided flag)
* `ifTests`: Dynamic branch evaluation details (test expression, boolean result, evaluation source)
* `syntax`: Druid syntax validation (`valid`, `dialect`, error messages)
* `execution`: Database execution results (when `execute: true`):
  * `executed`: Whether execution succeeded
  * `dataSource`: Datasource used
  * `executionTimeMs`: Execution duration in ms
  * `rowCount` / `affectedRows`: Rows returned or affected
  * `isDryRunRolledBack`: Whether transaction was rolled back
  * `columns`: Returned column names
  * `rows`: 2D array of data rows
* `warnings`: Warnings during processing

---

## `list_tables`

**Input**

* `projectPath`: Optional project path

**Output**

List of all configured data sources and table names (with data source names and JDBC URLs).

---

## `get_mybatis_generator_profile` / `set_mybatis_generator_profile`

Inspects or updates the project's MyBatis generator defaults (package names, source roots, Lombok switches, batch methods, etc.), allowing AI agents to generate code adhering to team standards.
---

# 📦 Configuration

The MyBatisCodeHelper-Pro plugin includes an internal MCP HTTP server (default port `63340`).

### Method 1: Generate `.mcp.json` (Recommended)

In IntelliJ IDEA:

```text
Tools
    └── MyBatisCodeHelper
            └── MCP Server
```

Click **Generate / Update .mcp.json in Project Root**.  
AI tools like Claude Code, Cursor, Cline, and Oh My Pi will automatically detect and connect to the MCP server.

Sample `.mcp.json`:

```json
{
  "mcpServers": {
    "mybatis": {
      "type": "http",
      "url": "http://127.0.0.1:63340/mcp"
    }
  }
}
```

### Method 2: Manual Configuration

Add the following configuration to your MCP-compatible assistant (e.g. cc-switch or global MCP settings):

Server name can be `MybatisMcp`:
```json
{
  "type": "http",
  "url": "http://127.0.0.1:63340/mcp"
}
```

> The MCP server is provided by the **MyBatisCodeHelper-Pro** IntelliJ IDEA plugin. Install the plugin and start the IDE first.
---

# 🚦 Starting the MCP Server

The MCP server is started manually inside IntelliJ IDEA.

## Method 1 (Recommended)

```text
Tools
    └── MyBatisCodeHelper
            └── Start MCP Server
```

A notification will appear in the IDE once the server has started.

---

## Method 2

```text
Settings / Preferences

Tools
    └── MyBatisCodeHelper
            └── MCP Server
                    └── Start
```

---

## Verify the Server Is Running

After startup, the menu item changes from

```text
Start MCP Server
```

to

```text
Stop MCP Server
```

indicating that the server is running and available to your AI coding assistant.

> The MCP server is available only while IntelliJ IDEA is running. Restart the server after reopening the IDE.

---

# 💡 Recommended Use Cases

| Scenario                           | MCP Tool                 |
| ---------------------------------- | ------------------------ |
| Locate a mapper XML                | `find_mapper_xml`        |
| Find the Java interface from XML   | `find_mapper_interface`  |
| List all database tables           | `list_tables`            |
| Inspect a table before writing SQL | `get_table_columns`      |
| Discover existing SQL statements   | `list_mapper_statements` |
| View configured data sources       | `list_data_sources`      |
| **Validate mapper syntax & contracts** | **`validate_mybatis_mapper`** |
| **Render / validate / execute SQL** | **`run_mybatis_sql`** |
| Generate CRUD from a table         | `generate_crud`          |
| Generate a mapper testcase         | `generate_mapper_testcase` |
| Query / set generator profile      | `get_mybatis_generator_profile` / `set_mybatis_generator_profile` |
---

# 📊 Key Benefits

1. **🎯 More Accurate** — Uses IntelliJ IDEA indexing and MyBatis metadata to locate mapper resources more reliably.
2. **📉 Smaller Context** — Returns structured metadata instead of entire XML files, reducing unnecessary context usage.
3. **⚡ Faster Responses** — Eliminates repeated file searches and XML parsing.
4. **💰 Lower Token Consumption** — Reduces unnecessary XML and schema reads during MyBatis development.
5. **📈 Better Scalability** — The larger your project, the greater the benefits of structured access through MCP.
