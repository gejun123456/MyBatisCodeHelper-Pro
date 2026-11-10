# MyBatis MCP：工具与客户端接入

通过插件内置的 MCP 服务，AI 可以按需读取项目 Mapper、数据库元数据和生成配置，并调用代码生成、静态校验与动态 SQL 求值工具，帮助减少手动提供上下文、重复解释规范和反复纠错的时间。

**[首次接入与任务演练](quickstart.md)** · [可复制的任务示例](ai-workflow.md) · [试用与购买](https://brucege.com/pay/view)

## 先看完整工作流程

| 阶段 | 工具 | 作用 |
| --- | --- | --- |
| 了解已有代码 | find_mapper_xml、find_mapper_interface、list_mapper_statements | 定位接口与 XML，读取现有语句信息 |
| 确认数据库 | list_data_sources、list_tables、get_table_columns | 查看可用连接、表与实际字段 |
| 遵循项目规范 | get_mybatis_generator_profile、set_mybatis_generator_profile | 读取或调整生成目录、包名与风格 |
| 生成代码 | generate_crud、generate_mapper_testcase | 写入业务代码或测试骨架 |
| 检查修改 | validate_mybatis_mapper | 检查语法、引用与映射，报告已执行及跳过的检查 |
| 验证指定输入 | run_mybatis_sql | 渲染动态 SQL、检查语法，按需连接数据库执行 |

按需查询上下文、调用工具生成和检查代码，有机会减少模型的重复读取与生成消耗。工具定义、调用与返回内容也占 Token，实际耗时和费用应按完整任务比较。[如何比较时间与 Token 消耗](ai-workflow.md#如何比较时间与-token-消耗)。

静态检查、SQL 渲染、数据库执行和测试断言验证的是不同内容。静态检查通过或测试骨架生成成功，都不代表业务结果已经验证。

---

## 🛠️ 提供的 MCP 工具

### 1. `find_mapper_xml` —— 根据 Java 接口查找 XML

**输入：**

Mapper 接口完全限定名（FQN）或 `.java` 文件路径

**输出：**

对应的 XML 文件路径列表

```text
输入：
com.example.mapper.UserMapper

输出：
src/main/resources/mapper/UserMapper.xml
```

> 一个项目中可能存在多个同名 XML（例如 `mapper/`、`easycode/` 等目录）。AI 自行搜索容易定位错误，而 MCP 基于 IntelliJ IDEA 的索引和 MyBatis 配置进行映射，能够更加可靠地定位正确的 XML。

---

### 2. `find_mapper_interface` —— 根据 XML 查找 Java 接口

**输入：**

XML 文件路径

**输出：**

对应的 Namespace 与 Java 接口

```text
输入：
src/main/resources/mapper/UserMapper.xml

输出：
com.example.mapper.UserMapper
```

---

### 3. `get_table_columns` —— 查询数据库表字段

**输入：**

表名

**输出：**

字段名称及对应 Java 类型

```text
user

id          → Long
username    → String
email       → String
create_time → Date
```

> AI 可直接通过 MCP 获取表结构，无需手动打开数据库客户端或查看 DDL。

---

### 4. `list_mapper_statements` —— 列出 Mapper SQL

**输入：**

Mapper 接口（FQN 或 `.java`）或 XML 文件

**输出：**

所有 SQL Statement

```text
selectByPrimaryKey   → select (line 28)
insert               → insert (line 40)
updateByPrimaryKey   → update (line 145)
deleteByPrimaryKey   → delete (line 35)
```

> 无需打开几百行 XML，即可快速了解当前 Mapper 包含哪些 SQL。

---

### 5. `list_data_sources` —— 查看项目数据源

**输入：**

无（或项目路径）

**输出：**

项目配置的数据源（名称、数据库类型、JDBC URL 等）

---

### 6. `generate_crud` —— 生成 CRUD 代码

**输入：**

- `table`：表名，必填
- `projectPath`：项目路径，可选；只打开一个项目时可以不传
- `dataSource`：数据源名称，可选；多个数据源时用于指定使用哪个数据源
- `modelName`：实体类名，可选；不传时使用项目配置的命名规则
- `referenceMapperXml`：参考 mapper xml，可选；会复用现有 XML / Mapper 的目录和包名布局
- `modelPackage` / `modelSrcRoot`：实体类包名和源码根目录，可选
- `mapperPackage` / `mapperSrcRoot`：Mapper 接口包名和源码根目录，可选
- `xmlPackage` / `xmlSrcRoot`：Mapper XML 路径和资源根目录，可选
- `servicePackage` / `serviceSrcRoot`：Service 实现类包名和源码根目录，可选
- `serviceInterfacePackage` / `serviceInterfaceSrcRoot`：Service 接口包名和源码根目录，可选
- `generateService` / `generateServiceInterface`：是否生成 Service / Service 接口，可选
- `insertMethod`、`insertSelective`、`selectByPrimaryKey`、`updateByPrimaryKey`、`updateByPrimaryKeySelective`、`deleteByPrimaryKey`：CRUD 方法开关，可选
- `batchInsert`、`updateBatch`、`updateBatchSelective`：批量方法开关，可选
- `useLombok`、`lombokGetterSetter`、`lombokBuilder`、`lombokAllArgs`、`lombokNoArgs`：Lombok 开关，可选
- `useCommonMapper`、`mapperAnnotation`、`mybatisFlex`、`addSchemaName`、`generateComment`、`useSwagger`、`noJdbcType`：框架和注解风格开关，可选
- `useMybatisPlus`、`mybatisPlusIdType`、`mybatisPlusStaticField`、`mybatisPlusGenerateByPrimaryKey`、`mybatisPlusGenerateUpdateAndInsertSelective`：MyBatis-Plus 3 相关开关，可选

**输出：**

- `status`
- `table`
- `modelName`
- `generatedFiles`
- `warnings`
- `modelPackage`
- `mapperPackage`
- `xmlPackage`

> 这是一个写入型工具，会直接在项目里生成实体类、Mapper 接口、Mapper XML，必要时也会生成 Service / Service 接口。路径解析顺序为：显式参数 > `referenceMapperXml` > 项目配置 / 模块默认值。风格开关不传时会使用当前项目 profile 中的默认配置。

---

### 7. `generate_mapper_testcase` —— 生成 Mapper 测试

**输入：**

- `mapper`：Mapper 接口 FQN 或 `.java` 路径，必填
- `projectPath`：项目路径，可选；只打开一个项目时可以不传
- `methodName`：Mapper 方法名，可选；不传时只生成测试类、mapper 字段和初始化方法
- `dataSource`：测试数据源，可选；会匹配项目中配置的数据源
- `testPackage`：测试类包名，可选；不传时默认使用 Mapper 所在包
- `testFramework`：测试框架，可选；支持 `JUNIT4` 或 `JUNIT5`

**输出：**

- `status`
- `testClassName`
- `testClassPath`
- `configurationPath`
- `generatedFiles`
- `warnings`

> 工具会创建或更新 Mapper 测试类、`setUpMybatisDatabase` 方法、mapper 字段，以及需要的 `mybatisTestConfiguration` XML。指定 `methodName` 时，会额外生成对应的测试方法；如果测试方法已经存在，会通过 `warnings` 返回提示。

支持运行命令返回的版本还会提供 `runCommand`、`runWorkingDirectory` 等信息（能识别构建工具时）。这是测试骨架：默认调用使用占位输入，未包含业务断言，测试配置可能自动提交写入。请先核对开发 / 测试连接、事务设置，补充有效输入、数据和断言，再执行并报告结果。

---

### 8. `validate_mybatis_mapper` —— 校验 Mapper XML 与 Java 接口契约

基于 IntelliJ IDEA 原生检查机制（DOM 校验、语言注入检验、OGNL 检查器及 SQL 解析器），对 MyBatis Mapper XML 与 Java 接口进行**深度静态契约校验**，无需启动 Spring 容器或执行任何测试即可发现语法与映射错误。

**核心校验能力：**
1. **IntelliJ DOM 深度校验（MapperDomElementInspection）：**
   - ResultMap 的 `property` 对应实体字段是否存在，支持普通属性、Getter/Setter、Lombok `@Data`、Kotlin 属性以及级联嵌套属性（如 `range.product.productId`）
   - `resultType` / `type` / `parameterType` 的类全限定名解析，支持 Spring Boot 类型别名及 MyBatis 内置基本类型别名
   - ResultMap ID 引用及 `<include refid="...">` 代码片段引用存在性
2. **语言注入校验（Injected Language Inspections）：**
   - `#{...}` 参数绑定检验（ParamLanguageInspection）：支持 `@Param` 注解、POJO 实体属性、Map 键值、List/数组集合参数绑定
   - `test="..."` OGNL 表达式引用检验（OgnlReferenceInspection）：支持 POJO 属性、静态方法调用（如 `@com.foo.Utils@isValid()`）、静态常量与内置变量
   - OGNL 常见语法陷阱检测（OgnlInspect）：如误将赋值 `=` 当作比较符、单字符字面量 `'1'` 匹配陷阱等
3. **XML 语法结构与原生 SQL 解析：**
   - 未闭合标签、非法属性等 XML 语法错误（自动捕获编辑器标红错误）
   - 静态 SQL 语法错误实时检测
4. **ResultMap 重复列名检测（ResultMapColumnDuplicateInspection）：**
   - 自动检测同一个 ResultMap 中映射重复 column 导致的数据覆盖问题
5. **Java 接口与 XML 契约一致性：**
   - 命名空间 namespace 是否与 Java 接口完全限定名一致
   - 接口中声明的方法是否缺少对应的 XML statement（已排除含 `@Select`/`@Update` 等注解的方法）
6. **数据库元数据联动（当配置了 IDE 数据源时）：**
   - 自动联动 IDE Database 数据源，检测 SQL 中引用的表名/列名是否存在
   - 检测 XML 中定义的 `jdbcType` 与数据库物理列类型是否匹配
7. **覆盖度契约与动态 SQL 评估（Coverage Contract）：**
   - 自动识别 `<if>`, `<choose>`, `<when>`, `<otherwise>`, `<where>`, `<trim>`, `<set>`, `<foreach>`, `${...}` 动态标签
   - **采用结构化覆盖度契约取代模糊的数值“置信度”**：在 `summary.checksExecuted` 中诚实列出所有已执行的静态检测项，在 `summary.checksSkipped` 中列出未执行的检测项（如未配置数据源时提示跳过表级校验；包含动态标签时提示静态分析无法穷举分支）。
   - **行动建议（recommendation）**：
     - `ALL_STATIC_PASSED`：语句为纯静态 SQL，已执行的静态检查未发现问题；仍需查看 `summary.checksSkipped`。该结论不证明运行时或业务结果正确，不能直接据此跳过相关测试
     - `STATIC_CHECKS_PASSED_WITH_DYNAMIC_SQL`：静态契约通过，但语句包含动态条件分支，提示 AI 配合 `run_mybatis_sql` 验证分支或编写多分支单测
     - `PASSED_WITH_WARNINGS`：静态契约通过，但存在警告（拼写可疑、类型不匹配），建议确认
     - `ERRORS_FOUND`：直接返回具体错误行号、错误描述和修复建议

**输入：**
- `mapper`：Mapper 接口全限定名（如 `com.example.mapper.UserMapper`）或 `.java` 文件路径（与 `xmlPath` 二选一）
- `xmlPath`：Mapper XML 文件路径（与 `mapper` 二选一）
- `statementId`：可选，指定单独校验某一条 statement ID；省略时校验当前 Mapper 中的所有 statement 与 resultMap
- `projectPath`：项目路径，可选（仅打开单一项目时可省略）

**输出：**
- `valid`：是否校验通过（`true` / `false`）
- `recommendation`：总体评估与下一步动作建议（`ALL_STATIC_PASSED` / `STATIC_CHECKS_PASSED_WITH_DYNAMIC_SQL` / `PASSED_WITH_WARNINGS` / `ERRORS_FOUND`）
- `summary`：统计信息（总语句数、静态语句数、动态语句数、总错误数、总警告数、`dynamicSqlNotice`，以及 `checksExecuted` 与 `checksSkipped` 清单）
- `resultMaps`：各个 ResultMap 的详细校验结果（字段匹配、错误及警告列表）
- `statements`：各个 Statement 的详细校验结果（包含 `hasDynamicSql`、`dynamicTags`、`sqlSyntax`、`sqlAnalysisNotice`、错误及警告列表）
- `globalErrors` / `globalWarnings`：命名空间不匹配、未实现接口方法等全局契约问题

```text
输入：
mapper: com.example.mapper.UserMapper

输出简要：
valid: true
recommendation: "ALL_STATIC_PASSED: All 4 statement(s) are pure static SQL and passed..."
summary: {
  "totalStatements": 4,
  "staticStatements": 4,
  "dynamicStatements": 0,
  "totalErrors": 0,
  "checksExecuted": ["xmlSyntax", "resultMapPropertyContract (DOM)", "parameterBinding (#{...})", "tableColumnResolution", ...],
  "checksSkipped": []
}
```

### 9. `run_mybatis_sql` —— 动态 SQL 求值渲染、语法校验与安全执行

提供**无需启动 Spring 容器或运行单测**的 Headless 动态 SQL 求值引擎，支持传参模拟、分支条件强制覆盖、Druid SQL 语法解析，以及连接真实数据库执行（支持事务自动回滚）。

**核心能力：**
- **动态 SQL 求值与渲染**：模拟 MyBatis 运行时求值逻辑，处理 `<if>`, `<choose>`, `<when>`, `<where>`, `<trim>`, `<set>`, `<foreach>`, `<bind>` 以及 `#{}` 参数替换与 `${}` 表达式拼接，渲染出真实可执行的标准 SQL。
- **分支覆盖与条件控制**：
  - 支持传入 `params`（如 `{"status": 1, "userId": 1001}`）自动进行 OGNL 求值
  - 支持传入 `ifTests` 精确覆盖特定 `<if test>` 条件（如 `{"status != null": true}`）
  - 支持 `allIfTestsTrue: true` 强制将 if 条件设为 true，检查该组合下的 SQL；这不等于覆盖所有条件组合
  - 支持 `allIfTestsFalse: true` 强制关闭全部动态分支（验证基础 SQL 语法）
- **Druid SQL 语法解析**：使用内置 Druid 语法解析器针对目标方言（MySQL, PostgreSQL, Oracle, SQLServer, H2, DB2 等）进行静态语法校验，检测关键字拼写、逗号缺失、括号不闭合等语法错误。
- **真实数据库安全执行（带 dryRun 回滚）**：
  - 自动复用 IntelliJ Database 工具窗口已保存的连接凭据，也可传入 `username`/`password` 临时覆盖
  - 查询类语句（SELECT）受 `maxRows` 行数保护（默认 50 条），防止大表数据撑爆 AI 上下文
  - 更新类语句（INSERT/UPDATE/DELETE）默认开启 `dryRun: true`，在事务中执行后**自动回滚**，可检查该输入下的数据库执行结果。事务回滚不能当作隔离环境，也不能保证消除所有副作用；请在开发 / 测试数据库使用真实执行。
- **多种声明载体支持**：不仅支持 XML 中的 `<select>`/`<update>` 标签，还支持 Java 接口上的 `@Select`/`@Update` 注解方法，甚至支持直接传入一段未保存的 `rawXml` 字符串片段进行测试。

**输入：**
- `mapper`：Mapper 接口全限定名或 `.java` 路径，可选
- `methodName` / `statementId`：方法名或 XML 语句 ID，可选
- `xmlPath`：Mapper XML 文件路径，可选
- `rawXml`：直接传入原生 XML 语句片段（如 `<select id="find">SELECT * FROM user WHERE id = #{id}</select>`），可选
- `params`：传参键值对对象（如 `{"id": 1, "status": "ACTIVE"}`），可选
- `ifTests`：显式指定 `<if test="...">` 条件布尔值映射（如 `{"status != null": true}`），可选
- `allIfTestsTrue`：强制将所有动态 `<if test>` 条件求值为 true，可选
- `allIfTestsFalse`：强制将所有动态 `<if test>` 条件求值为 false，可选
- `format`：是否对渲染出的 SQL 进行排版格式化（默认 `true`）
- `checkSyntax`：是否使用 Druid 解析器校验渲染后的 SQL 语法（默认 `true`）
- `execute`：是否连接数据库真实执行该 SQL（默认 `false`）
- `dryRun`：执行 DML（插入/更新/删除）后是否自动回滚事务（默认 `true`）
- `dataSource`：目标数据源名称，可选（多数据源时指定）
- `maxRows`：查询最大返回行数（默认 `50`，范围 1~1000）
- `dbType`：SQL 方言（如 `mysql`, `postgresql`, `oracle`, `sqlserver`, `h2`，默认自动检测）
- `username` / `password`：可选的数据库账号密码覆盖

**输出：**
- `status`：`success` 或 `error`
- `statementId` / `statementType`：语句 ID 及类型（select/insert/update/delete）
- `renderedSql`：最终渲染出的完整可执行 SQL
- `parameters`：参数使用详情（参数名、属性、实际使用的值、默认值来源）
- `ifTests`：每个 `<if test>` 条件的求值结果及判定来源（`explicit`, `allIfTestsTrue`, `ognl`, `fallback`）
- `syntax`：Druid 语法校验结果（`valid`, `statementType`, `dialect`, `error`）
- `execution`：数据库执行结果（`executed`, `dataSource`, `executionTimeMs`, `rowCount`, `affectedRows`, `isDryRunRolledBack`, `columns`, `rows`, `error`）

---

### 10. `list_tables` —— 查看数据库表列表

查询 IntelliJ IDEA Database 工具窗口中配置的数据源与可见数据库表列表，帮助 AI 在生成 CRUD 或编写 SQL 前了解当前项目有哪些表可用。

**输入：**
- `projectPath`：项目路径，可选

**输出：**
- `dataSources`：数据源列表，包含数据源名称、JDBC URL、表列表（表名、Schema、表数量等）

---

### 11. `get_mybatis_generator_profile` —— 读取代码生成器配置

读取当前项目的 MyBatis generator 默认配置（ProjectProfile），包括实体/Mapper/XML/Service/Controller 的包名与源码目录、文件前后缀、开关设置（Lombok, Swagger, MyBatis-Plus/Flex 等）以及模块路径映射。

**输入：**
- `projectPath`：项目路径，必填

**输出：**
- 项目级默认路径、包名、命名规则前后缀、功能开关配置、模块专属路径映射列表，以及可能缺失的配置字段提示。

---

### 12. `set_mybatis_generator_profile` —— 设置代码生成器配置

更新当前项目的 MyBatis generator 配置（ProjectProfile），支持设置模块专属目录或全局配置，便于在通过 MCP 生成 CRUD 或打开生成弹窗时保持统一的工程规范。

**输入：**
- `projectPath`：项目路径，必填
- `moduleName`：可选，指定针对某个子模块设置路径信息
- `modelPackage` / `modelSrcRoot`：实体类包名及源码根路径
- `mapperPackage` / `mapperSrcRoot`：Mapper 接口包名及源码根路径
- `xmlPackage` / `xmlSrcRoot`：Mapper XML 路径及资源根路径
- `servicePackage` / `serviceSrcRoot`：Service 实现类包名及源码根路径
- `serviceInterfacePackage` / `serviceInterfaceSrcRoot`：Service 接口包名及源码根路径
- `controllerPackage` / `controllerSrcRoot`：Controller 类包名及源码根路径
- `mapperSuffix` / `mapperPrefix` / `modelPrefix` / `xmlPrefix` / `xmlSuffix`：文件命名规范
- 开关字段：`useLombok`, `mapperAnnotation`, `useMybatisPlus`, `mybatisFlex`, `useSwagger`, `noJdbcType`, `generateComment`, `generateService`, `generateServiceInterface`, `generateController`, `database` 等

**输出：**
- `status`、更新提示信息及实际变更的字段列表（`changedFields`）。

---

## 生成 AI Skill

支持此功能的版本提供 **Generate MyBatis AI Skill (SKILL.md)**：可从 Tools → MyBatisCodeHelper、MCP 启动窗口或 MCP 设置页打开。选择实际使用的客户端后生成，再按提示重载客户端或项目。

| 客户端 | 项目内生成位置 |
| --- | --- |
| Claude Code | .claude/skills/mybatis-code-helper/SKILL.md |
| CodeBuddy | .codebuddy/skills/mybatis-code-helper/SKILL.md |
| WorkBuddy | .workbuddy/skills/mybatis-code-helper/SKILL.md |
| Cursor | .cursor/rules/mybatis-code-helper.mdc |

Skill 包含工具使用流程、参数参考与常见问题；生成时写入当前服务地址。它指导 AI 先读取上下文，再修改并验证。MCP 连接和 Skill 加载需分别确认。生成操作会覆盖相同路径下的同名 Skill / 规则文件，请先查看预览。

如果安装版本尚无此按钮，可先使用 [任务提示词](ai-workflow.md)，并在 Marketplace 的版本记录中确认功能可用性。

### WorkBuddy 接入

支持此功能的版本可在 MCP 窗口或设置页使用“写入 WorkBuddy”，将 mybatis HTTP 服务合并到用户的 ~/.workbuddy/mcp.json，保留已有服务；不合法的 JSON 不会被覆盖。写入后按提示重启或重新打开项目，并确认工具可见。此连接配置与项目内 Skill 是两项独立配置。

---

## 📦 配置与客户端接入

MyBatisCodeHelper-Pro 内置了符合标准 Streamable-HTTP 规范的 MCP Server（默认监听端口 `http://127.0.0.1:63340/mcp`）。

### ⚡ 一键生成项目配置（推荐）

启动 MCP 服务后，在弹出的配置指引窗口中，点击 **「一键生成 / 更新项目 .mcp.json (Oh My Pi / 通用)」**，即可自动在当前项目根目录下生成或更新 `.mcp.json`：

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

此文件适用于支持项目 `.mcp.json` 的客户端。不同客户端的配置路径与启用流程不同，请按启动窗口或客户端说明接入，并在客户端确认服务已连接、工具可见。

---

### 各 AI 客户端手动配置指引

#### 1. Oh My Pi / 通用项目配置 (.mcp.json)

在项目根目录下创建 `.mcp.json`：

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

直接在终端执行添加命令：

```bash
claude mcp add --transport http mybatis http://127.0.0.1:63340/mcp
```

#### 3. Cursor / Windsurf

在 **Settings -> MCP -> Add new MCP server** 中配置：

```text
Name: mybatis
Type: http
URL:  http://127.0.0.1:63340/mcp
```

#### 4. 仅支持 stdio 的客户端桥接

对于只支持 stdio 传输协议的客户端，可以通过 `mcp-remote` 将 HTTP 端点转为 stdio（以下为 TOML 配置格式示例，实际配置文件位置以客户端为准）：

```toml
[mcp_servers.mybatis]
command = "npx"
args = ["-y", "mcp-remote", "http://127.0.0.1:63340/mcp"]
```

#### 5. cc-switch

直接粘贴服务配置：

```json
{
  "mybatis": {
    "type": "http",
    "url": "http://127.0.0.1:63340/mcp"
  }
}
```

---

## 🚦 启动与管理 MCP 服务

MyBatisCodeHelper-Pro 提供两种启动方式：

### 方式一：顶部菜单（推荐）

```text
Tools
    └── MyBatisCodeHelper
            └── Start MyBatis MCP Server
```

启动成功后会弹出交互式配置指引弹窗（McpServerDialog），可一键生成 `.mcp.json` 或复制接入命令。

---

### 方式二：设置页面

```text
Settings / Preferences

Tools
    └── MyBatisCodeHelper
            └── MCP Server
                    └── Start
```

在设置页面中可以修改监听端口（默认 63340）以及管理运行状态。

---

### 如何确认已启动

启动成功后，菜单项会由

```text
Start MyBatis MCP Server
```

变为

```text
Stop MyBatis MCP Server
```

说明服务已经运行，此时 AI 编码助手即可通过 MCP 与当前项目进行交互。

> MCP 服务依赖 IntelliJ IDEA 运行。保持目标项目打开、索引完成，并确认服务正在运行。

---

## 💡 推荐使用场景

| 场景 | 推荐工具 | 优势说明 |
| --- | --- | --- |
| 快速定位 XML | `find_mapper_xml` | 精准匹配，避免同名文件定位错误 |
| 根据 XML 找接口 | `find_mapper_interface` | 双向契约直达 |
| 编写 SQL 前查看表结构 | `get_table_columns` | 获取精准字段与 Java 映射类型 |
| 查看已有 SQL | `list_mapper_statements` | 无需读取大体积 XML，直接返回语句元数据 |
| 查看所有数据库表 | `list_tables` | 按数据源和 schema 列出全部表 |
| 查看项目数据源 | `list_data_sources` | 了解当前配置的数据库连接 |
| **静态校验 Mapper 与 XML 契约** | `validate_mybatis_mapper` | **深度检测属性映射、OGNL、参数绑定，标红语法错误** |
| 查看校验覆盖范围 | `validate_mybatis_mapper` | 查看 checksExecuted 与 checksSkipped，确定还需执行的验证 |
| **动态 SQL 求值与渲染** | `run_mybatis_sql` | 按指定参数求值与渲染 SQL |
| **SQL 真实语法与分支覆盖** | `run_mybatis_sql` | 检查指定参数或条件覆盖设置下的语法，不代表全部分支组合通过 |
| **真实数据库安全执行** | `run_mybatis_sql` | 在开发 / 测试库执行指定输入；DML 支持 dryRun 回滚 |
| 根据表生成 CRUD 代码 | `generate_crud` | 直接生成实体、Mapper、XML 及 Service |
| 生成 Mapper 单元测试 | `generate_mapper_testcase` | 自动配置 H2/真实库测试用例 |
| 读取代码生成规则 | `get_mybatis_generator_profile` | 获取包名、路径规范与代码风格 |
| 设置代码生成规则 | `set_mybatis_generator_profile` | 统一团队工程目录规范 |
---

## 接下来

[完成第一个 AI 任务](quickstart.md) · [更多任务示例](ai-workflow.md) · [功能与版本对比](features.md) · [试用与购买](https://brucege.com/pay/view)
