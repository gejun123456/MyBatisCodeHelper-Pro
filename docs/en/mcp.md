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
Performs **deep static contract validation** of MyBatis mapper XML and Java interfaces using IntelliJ IDEA's native inspection framework (DOM validation, language injection inspections, OGNL inspection, and native SQL parsing). Detects syntax and mapping errors without starting the Spring context or executing unit tests.

**Key Validation Capabilities:**
1. **IntelliJ DOM Deep Validation (`MapperDomElementInspection`):**
   * ResultMap `property` existence on entity classes, supporting regular fields, getters/setters, Lombok `@Data`, Kotlin properties, and nested cascade properties (e.g. `range.product.productId`)
   * Class resolution for `resultType`, `type`, and `parameterType`, with full support for Spring Boot type-aliases and MyBatis built-in aliases
   * ResultMap ID reference resolution and `<include refid="...">` SQL snippet reference validation
2. **Injected Language Inspections:**
   * `#{...}` parameter binding validation (`ParamLanguageInspection`), supporting `@Param` annotations, POJO properties, Maps, and collections
   * `test="..."` OGNL expression validation (`OgnlReferenceInspection`), supporting POJO properties, static method calls (e.g. `@com.foo.Utils@isValid()`), static fields, and built-in variables
   * OGNL syntax traps detection (`OgnlInspect`), such as accidental assignment operator `=` instead of comparison, and character literal matching traps
3. **XML Syntax & Native SQL Parsing:**
   * Real-time editor error detection for unclosed tags, malformed XML attributes, and invalid SQL statements
4. **ResultMap Duplicate Column Detection (`ResultMapColumnDuplicateInspection`):**
   * Detects duplicate column mappings in the same ResultMap that could cause data overwrites
5. **Java-XML Contract Consistency:**
   * Verifies that the XML namespace matches the fully qualified name of the Java interface
   * Identifies interface methods missing corresponding XML statements (excluding annotated methods like `@Select`/`@Update`)
6. **Database Schema Resolution (when IDE data source is configured):**
   * Resolves table and column names in SQL statements against the IDE Database tool window
   * Validates `jdbcType` vs. physical DB column type compatibility
7. **Coverage Contract & Dynamic SQL Assessment:**
   * Automatically detects dynamic SQL tags: `<if>`, `<choose>`, `<when>`, `<otherwise>`, `<where>`, `<trim>`, `<set>`, `<foreach>`, and `${...}` substitutions
   * **Structured Coverage Contract**: Replaces ambiguous numeric scores with explicit `checksExecuted` and `checksSkipped` lists in `summary`
   * **Actionable Recommendations**:
     * `ALL_STATIC_PASSED`: All statements are deterministic static SQL and pass all static contract checks. AI can be certain the SQL is 100% correct, **safely skipping unit test execution** and saving development time and tokens.
     * `STATIC_CHECKS_PASSED_WITH_DYNAMIC_SQL`: Static contracts passed, but due to conditional runtime branches, recommends using `run_mybatis_sql` for dynamic branch evaluation or writing unit tests covering branch permutations.
     * `PASSED_WITH_WARNINGS`: Static contracts passed, but warnings indicate potential defects (e.g., suspicious typos, mismatched types).
     * `ERRORS_FOUND`: Returns line numbers, error descriptions, and actionable fix suggestions.

**Input**
* `mapper`: fully qualified mapper class name (e.g. `com.example.mapper.UserMapper`) or `.java` file path (use this or `xmlPath`)
* `xmlPath`: mapper XML file path (use this or `mapper`)
* `statementId`: optional statement ID to validate specifically; if omitted, all statements and resultMaps in the mapper are validated
* `projectPath`: optional absolute project path when multiple projects are open

**Output**
* `valid`: boolean (`true` / `false`)
* `recommendation`: overall assessment and suggested next step (`ALL_STATIC_PASSED`, `STATIC_CHECKS_PASSED_WITH_DYNAMIC_SQL`, `PASSED_WITH_WARNINGS`, `ERRORS_FOUND`)
* `summary`: statistics (total statements, static statements, dynamic statements, total errors, total warnings, `dynamicSqlNotice`, plus `checksExecuted` and `checksSkipped` lists)
* `resultMaps`: detailed validation breakdown for each ResultMap
* `statements`: detailed validation breakdown for each statement (including `hasDynamicSql`, `dynamicTags`, `sqlSyntax`, `sqlAnalysisNotice`, errors, warnings)
* `globalErrors` / `globalWarnings`: namespace mismatches, unmapped interface methods, and file-level issues
---

## `run_mybatis_sql`

A headless dynamic SQL evaluation engine for rendering, validating syntax, and safely executing MyBatis statements **without starting a Spring container or test runner**.

**Key Capabilities:**
* **Dynamic SQL Evaluation & Rendering**: Simulates MyBatis runtime tag evaluation (`<if>`, `<choose>`, `<when>`, `<where>`, `<trim>`, `<set>`, `<foreach>`, `<bind>`), replaces `#{}` parameter placeholders, and interpolates `${}` expressions into clean, formatted SQL.
* **Branch Coverage & Conditional Overrides**:
  * Supply `params` (e.g. `{"status": 1, "userId": 1001}`) for automatic OGNL evaluation
  * Override specific `<if test="...">` conditions via `ifTests` (e.g. `{"status != null": true}`)
  * Use `allIfTestsTrue: true` to force all dynamic branches active (verifies full syntax coverage)
  * Use `allIfTestsFalse: true` to evaluate baseline SQL without dynamic branches
* **Druid SQL Syntax Validation**: Automatically parses rendered SQL using the Druid parser for target dialects (MySQL, PostgreSQL, Oracle, SQLServer, H2, DB2, etc.) to catch syntax errors, missing commas, or misplaced keywords.
* **Safe Database Execution with Dry-Run Rollback**:
  * Reuses database credentials configured in IntelliJ's Database tool window, or accepts `username`/`password` overrides
  * SELECT queries are capped by `maxRows` (default 50) to protect conversation context
  * DML statements (INSERT, UPDATE, DELETE) default to `dryRun: true`, executing inside a transaction that is **automatically rolled back**, proving database compatibility without corrupting real data.
* **Multiple SQL Sources**: Supports XML statement tags, `@Select`/`@Update` Java annotations, or direct uncommitted `rawXml` snippets.

**Input**
* `mapper`: mapper interface FQN or `.java` path (optional)
* `methodName` / `statementId`: method name or statement ID (optional)
* `xmlPath`: mapper XML path (optional)
* `rawXml`: direct XML statement snippet (e.g. `<select id="find">SELECT * FROM user WHERE id = #{id}</select>`) (optional)
* `params`: parameter key-value pairs (e.g. `{"id": 1, "status": "ACTIVE"}`) (optional)
* `ifTests`: explicit boolean overrides for `<if test="...">` expressions (e.g. `{"status != null": true}`) (optional)
* `allIfTestsTrue`: force all dynamic conditions to true (optional)
* `allIfTestsFalse`: force all dynamic conditions to false (optional)
* `format`: format rendered SQL with indentation (default `true`)
* `checkSyntax`: validate rendered SQL syntax using Druid parser (default `true`)
* `execute`: execute rendered SQL against project database (default `false`)
* `dryRun`: rollback DML statements after execution (default `true`)
* `dataSource`: target datasource name (optional)
* `maxRows`: maximum rows to return for queries (default `50`, max 1000)
* `dbType`: SQL dialect (`mysql`, `postgresql`, `oracle`, `sqlserver`, `h2`, default auto-detected)
* `username` / `password`: optional credentials override

**Output**
* `status`: `success` or `error`
* `statementId` / `statementType`: statement ID and type (select/insert/update/delete)
* `renderedSql`: standard formatted SQL ready for execution
* `parameters`: detailed parameter usage and fallback values
* `ifTests`: evaluated condition results and resolution source (`explicit`, `allIfTestsTrue`, `ognl`, `fallback`)
* `syntax`: Druid parser validation result (`valid`, `statementType`, `dialect`, `error`)
* `execution`: database execution details (`executed`, `dataSource`, `executionTimeMs`, `rowCount`, `affectedRows`, `isDryRunRolledBack`, `columns`, `rows`, `error`)

---

## `list_tables`

Lists all database tables visible in the IDE's Database tool window, helping AI coding assistants know which tables and schemas exist before calling `get_table_columns` or `generate_crud`.

**Input**
* `projectPath`: optional absolute project path

**Output**
* `dataSources`: list of data sources with name, JDBC URL, and table metadata (table name, schema, table count)

---

## `get_mybatis_generator_profile`

Reads the project's current MyBatis generator defaults (`ProjectProfile`), including packages, source roots, naming suffixes/prefixes, generator switches (Lombok, Swagger, MyBatis-Plus/Flex, etc.), and module-specific path mappings.

**Input**
* `projectPath`: absolute project path (required)

**Output**
* Default paths, packages, naming conventions, feature switches, module mappings, and warnings for missing fields.

---

## `set_mybatis_generator_profile`

Updates the project's MyBatis generator defaults (`ProjectProfile`), setting global or module-specific paths and generator switches.

**Input**
* `projectPath`: absolute project path (required)
* `moduleName`: optional submodule name for module-specific configuration
* `modelPackage` / `modelSrcRoot`: entity package and source directory
* `mapperPackage` / `mapperSrcRoot`: mapper interface package and source directory
* `xmlPackage` / `xmlSrcRoot`: mapper XML package and resource directory
* `servicePackage` / `serviceSrcRoot`: service implementation package and source directory
* `serviceInterfacePackage` / `serviceInterfaceSrcRoot`: service interface package and source directory
* `controllerPackage` / `controllerSrcRoot`: controller package and source directory
* `mapperSuffix` / `mapperPrefix` / `modelPrefix` / `xmlPrefix` / `xmlSuffix`: naming conventions
* Switches: `useLombok`, `mapperAnnotation`, `useMybatisPlus`, `mybatisFlex`, `useSwagger`, `noJdbcType`, `generateComment`, `generateService`, `generateServiceInterface`, `generateController`, `database`

**Output**
* `status`, update message, and list of `changedFields`.

---

# 📦 Configuration & Client Setup

MyBatisCodeHelper-Pro includes an embedded MCP server speaking the standard Streamable-HTTP transport (default endpoint: `http://127.0.0.1:63340/mcp`).

### ⚡ One-Click Project Configuration (Recommended)

When the MCP server starts, the configuration dialog provides a **"Generate / Update .mcp.json in Project Root (Oh My Pi / Universal)"** button. Clicking it creates or updates `.mcp.json` in your project root:

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

AI tools like **Oh My Pi**, **Claude Code**, and **Cursor** automatically discover and connect to the MyBatis MCP server when opening the project.

---

### Manual Setup by Client

#### 1. Oh My Pi / Universal Project Config (`.mcp.json`)

Place `.mcp.json` in your project root directory:

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

#### 2. Claude Code

Run the registration command in your terminal:

```bash
claude mcp add --transport http mybatis http://127.0.0.1:63340/mcp
```

#### 3. Cursor / Windsurf

Navigate to **Settings -> MCP -> Add new MCP server**:

```text
Name: mybatis
Type: http
URL:  http://127.0.0.1:63340/mcp
```

#### 4. Codex / stdio Bridge (DeepSeek CLI / Python)

For clients supporting only stdio transport, bridge the HTTP endpoint using `mcp-remote` (e.g. in `~/.codex/config.toml`):

```toml
[mcp_servers.mybatis]
command = "npx"
args = ["-y", "mcp-remote", "http://127.0.0.1:63340/mcp"]
```

#### 5. cc-switch

Paste the raw JSON server entry:

```json
{
  "mybatis": {
    "type": "http",
    "url": "http://127.0.0.1:63340/mcp"
  }
}
```

---

# 🚦 Starting & Managing the MCP Server

## Method 1: Tools Menu (Recommended)

```text
Tools
    └── MyBatisCodeHelper
            └── Start MCP Server
```

Starting the server opens an interactive configuration dialog (McpServerDialog) with one-click `.mcp.json` generation and connection commands for various clients.

---

## Method 2: Settings Page

```text
Settings / Preferences

Tools
    └── MyBatisCodeHelper
            └── MCP Server
                    └── Start
```

Configure the listening port (default 63340) and monitor server status.

---

## Verify Server Status

After startup, the menu item toggles from

```text
Start MCP Server
```

to

```text
Stop MCP Server
```

indicating the server is running.

> The MCP server runs inside IntelliJ IDEA. When the IDE closes, the server stops and should be restarted after reopening.

---

# 💡 Recommended Use Cases

| Scenario | Recommended Tool | Advantage |
| --- | --- | --- |
| Locate a mapper XML | `find_mapper_xml` | Reliable lookup avoiding same-name file confusion |
| Find Java interface from XML | `find_mapper_interface` | Direct two-way navigation |
| Inspect schema before writing SQL | `get_table_columns` | Accurate column types mapped to Java types |
| List existing SQL statements | `list_mapper_statements` | Structured statement metadata without XML parsing |
| List all database tables | `list_tables` | Full table inventory grouped by data source & schema |
| View project data sources | `list_data_sources` | Inspect configured JDBC connections |
| **Static Mapper & XML Contract Validation** | `validate_mybatis_mapper` | **Deep checks for property mapping, OGNL expressions, and syntax errors** |
| **Pure Static SQL Skip-Test Assessment** | `validate_mybatis_mapper` | **ALL_STATIC_PASSED safely skips unit tests, saving tokens and time** |
| **Dynamic SQL Branch Evaluation** | `run_mybatis_sql` | **Zero-overhead dynamic tag rendering with parameter simulation** |
| **SQL Syntax & Branch Verification** | `run_mybatis_sql` | **Druid syntax parser validation with branch override options** |
| **Safe Real Database Execution** | `run_mybatis_sql` | **Automatic dryRun transaction rollback for DML statements** |
| Generate CRUD from a table | `generate_crud` | Generates entity, mapper, XML, and service code |
| Generate mapper testcase | `generate_mapper_testcase` | Sets up H2 or real database test suites |
| Read generator settings | `get_mybatis_generator_profile` | Inspects project code style and package rules |
| Set generator settings | `set_mybatis_generator_profile` | Synchronizes project configuration standards |
---

# 📊 Key Benefits

1. **🎯 Deep Static Contract Validation** — Leverages IntelliJ IDEA's native DOM and language injection subsystems to validate ResultMap property mappings, OGNL syntax, and `#{}` parameter bindings. Pure static SQL can skip unit tests with 1.0 confidence.
2. **⚡ Headless Dynamic SQL Evaluation & Safe Execution** — Evaluates dynamic `<if>`/`<choose>` branches, validates SQL syntax via Druid parser, and executes queries against real databases with automatic dry-run rollback.
3. **📉 Maximum Context Conservation** — Delivers compact structured JSON, eliminating the need to feed large XML documents into AI context windows.
4. **🛠️ Complete Generation & Engineering Workflow** — Reads and writes code generation profiles, scaffolding complete CRUD implementations and test suites.
5. **🔌 Universal AI Tool Compatibility** — Offers one-click `.mcp.json` generation and works out of the box with Oh My Pi, Claude Code, Cursor, Windsurf, Codex, and cc-switch.
