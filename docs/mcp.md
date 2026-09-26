# MyBatis MCP (Model Context Protocol) 支持

MyBatisCodeHelper-Pro 提供了 **MCP (Model Context Protocol)** 支持，让 AI 编码助手（如 Claude Code）能够直接与你的 MyBatis 项目交互，大幅提升开发效率。

---

## 🚀 为什么使用 MyBatis MCP？

AI 编码助手在处理 MyBatis 项目时，经常需要查找 Mapper 接口对应的 XML 文件、查看数据库表结构、分析 SQL 语句。**没有 MCP 时**，AI 通常需要搜索项目文件、读取 XML 内容，再从中提取所需信息，不仅消耗更多 Token，也会占用大量上下文窗口。

### 有 MCP vs 无 MCP

| 操作                | 无 MCP                                        | 有 MCP                         |                 节省                 |
| ----------------- | -------------------------------------------- | ----------------------------- | :--------------------------------: |
| 查 Mapper → XML 映射 | 搜索项目并确认映射（约 150~250 Tokens）                  | **一次 MCP 调用（约 30~60 Tokens）** |        **约 100~200 Tokens**        |
| 查看 Mapper SQL 列表  | 通常需要读取 XML 文件（约 1000~2500 Tokens，视 XML 大小而定） | **直接返回结构化 SQL 列表**            |       **约 1000~2500 Tokens**       |
| 查询数据库表字段          | 打开数据库工具或读取 DDL（约 300~500 Tokens）             | **一次 MCP 调用（约 50 Tokens）**    |        **约 250~450 Tokens**        |
| 校验 Mapper 契约与语法   | 人肉阅读长 XML 易漏看，且常出现 OGNL / 类型幻觉           | **深度静态契约检测，毫秒级定位标签/参数/类型错误** | **大幅避免动态 SQL 暗坑与繁琐排错**  |
| 动态 SQL 模拟与安全执行 | 手写单测启动 Spring 上下文或脑补分支拼接结果              | **支持分支求值、参数模拟、Druid 校验与 DryRun** | **秒级验证，无需启动复杂测试容器**    |
| MyBatis 相关开发流程    | 多次搜索、读取 XML、查看表结构                            | **直接调用 MCP 获取所需信息**           | **通常可减少 60%~90% 的 MyBatis 相关信息读取** |
> 查找文件本身节省有限，但读取 XML、查看 SQL、查询表结构等操作能够显著减少 Token 消耗。随着查询次数增加，整体收益会越来越明显。

---

## 📉 减少上下文占用

没有 MCP 时，AI 往往需要把整个 XML 文件读入当前会话上下文。

例如一个对话涉及 3 个不同的 Mapper：

```text
无 MCP：
3 × 约 2000 Tokens
≈ 6000 Tokens 的 XML 内容持续占用当前会话上下文

有 MCP：
3 × 约 50 Tokens
≈ 150 Tokens 的结构化数据
```

节省约 **5800 Tokens** 的上下文空间。

上下文越干净，模型越容易关注真正需要的信息，而不是大量 XML 内容，因此回答通常也会更加准确。

---

## 📈 项目越大，收益越明显

| 项目规模 | 典型 XML 大小 |       单次读取 XML      |     涉及 5 个 Mapper    |
| :--- | :-------: | :-----------------: | :------------------: |
| 小型项目 |  5~10 KB  |  约 1000~2500 Tokens |  约 5000~12500 Tokens |
| 中型项目 |  15~30 KB |  约 4000~7500 Tokens | 约 20000~37500 Tokens |
| 大型项目 |  30~50 KB | 约 7500~12500 Tokens | 约 37500~62500 Tokens |

> XML 越大，AI 每次读取消耗的 Token 越多。MCP 返回结构化数据，因此项目规模越大，优势越明显。

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

---

### 8. `validate_mybatis_mapper` —— 校验 Mapper XML 与 Java 接口契约

利用 IntelliJ IDEA 深度静态分析框架（DOM 模型校验、MyBatis Param 语言解析、OGNL 表达式检查等），对 MyBatis Mapper XML 及其 Java 接口进行全方位的静态契约校验，在代码提交或运行前及早拦截潜在缺陷。

**检测范围：**

* **XML 结构与语法**：根节点合法性、标签闭合及格式问题
* **DOM 映射契约**：`resultType` 类是否存在、`resultMap` 映射属性是否存在于实体类、`association`/`collection` 嵌套映射正确性
* **参数绑定检测**：`#{...}` 占位符与 Java 接口 `@Param` 参数或实体类 Getter 属性的一致性
* **OGNL 表达式检测**：`<if test="...">`、`<when test="...">` 中的变量引用与语法规范
* **SQL 片段引用**：`<include refid="...">` 引用的存在性（支持当前文件及跨命名空间）
* **Java-XML 一致性**：接口与 XML 命名空间对应关系、方法与 XML Statement ID 互相映射检测
* **纯静态 SQL 语法校验**：基于 IntelliJ SQL 解析器检测语法错误
* **数据库元数据联动（当配置了 IDE 数据源时）**：检测 SQL 中引用的表名/字段是否存在，以及 `jdbcType` 与数据库物理列类型是否匹配

> **覆盖度契约与动态 SQL 评估**：  
> 包含 `<if>`、`<choose>`、`<foreach>` 等动态标签的语句，静态分析无法穷举所有运行时分支组合。该工具通过 `checksExecuted` 与 `checksSkipped` 诚实反馈已执行和跳过的检查项，并在包含动态标签时给出 `STATIC_CHECKS_PASSED_WITH_DYNAMIC_SQL` 等明确建议，指引配合 `run_mybatis_sql` 或编写单测验证分支。

**输入：**

* `mapper`：Mapper 接口完全限定名（FQN，例如 `com.example.mapper.UserMapper`）或 `.java` 路径（与 `xmlPath` 二选一）
* `xmlPath`：Mapper XML 文件路径（与 `mapper` 二选一）
* `statementId`：可选。仅校验指定的 Statement ID；不传则校验该 XML/接口下的所有 statement 和 resultMap
* `projectPath`：项目路径，可选；只打开一个项目时可以不传

**输出：**

* `valid`：是否通过校验（无阻断性错误时为 `true`）
* `recommendation`：行动指引，例如：
  * `ALL_STATIC_PASSED`：纯静态 SQL，执行的所有静态契约校验全部通过
  * `STATIC_CHECKS_PASSED_WITH_DYNAMIC_SQL`：静态契约通过，但语句包含动态标签，建议编写测试用例或使用 `run_mybatis_sql` 验证分支
  * `PASSED_WITH_WARNINGS`：静态契约通过，但存在警告（拼写可疑、类型不匹配等），建议确认
  * `ERRORS_FOUND`：发现错误，必须修复
* `summary`：包含总语句数、静态语句数、动态语句数、错误数、警告数，以及 `checksExecuted`（已执行检查列表）和 `checksSkipped`（跳过检查列表及原因）
* `statements`：各 Statement 详细校验信息（包含动态标签列表、`sqlAnalysisNotice` 提示、错误与警告等）
* `resultMaps`：ResultMap 映射与字段属性检测结果
* `globalErrors` / `globalWarnings`：全局/文件级错误与警告

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
  "checksExecuted": ["xmlSyntax", "resultMapPropertyContract (DOM)", "parameterBinding (#{...})", "tableColumnResolution", ...]
}
```

---

### 9. `run_mybatis_sql` —— 动态 SQL 模拟渲染、语法校验与安全执行

零开销模拟 MyBatis 动态 SQL 执行，**无需启动 Spring 容器或准备复杂测试用例**！

支持动态标签求值（`<if>`, `<choose>`, `<where>`, `<trim>`, `<foreach>`, OGNL 表达式）、参数注入、Druid AST 语法解析以及针对 IDE 数据源的实际 SQL 执行（支持事务回滚 dryRun、结果集预览与最大行数限制）。

无论是由 AI 生成的代码片段需要快速验证，还是排查现有复杂动态 SQL 在不同参数组合下的拼装结果，都能秒级完成。

**输入：**

* **定位方式（选其一）：**
  * `xmlPath` + `statementId`（或 `methodName`）：通过 XML 文件路径与语句 ID 定位
  * `mapper` + `methodName`（或 `statementId`）：通过 Mapper 接口与方法名定位
  * `rawXml`：直接传入一段 XML 语句代码片段（例如 `<select id="find">SELECT * FROM user WHERE id = #{id}</select>`），无需落盘即可即时验证
* **参数模拟与分支控制：**
  * `params`：模拟传入的参数键值对（JSON 对象，例如 `{"id": 1, "status": "ACTIVE"}`）
  * `ifTests`：显式指定特定 `<if test="...">` 条件的布尔值（例如 `{"status != null": true, "name != null": false}`）
  * `allIfTestsTrue`：布尔值，强制所有 `<if test>` 条件全部为 `true`（用于验证全分支拼接）
  * `allIfTestsFalse`：布尔值，强制所有 `<if test>` 条件全部为 `false`（用于验证空条件基线）
* **执行与校验控制：**
  * `format`：布尔值，是否对渲染后的 SQL 进行格式化美化（默认 `true`）
  * `checkSyntax`：布尔值，是否使用 Druid 语法解析器校验渲染后的 SQL（默认 `true`）
  * `execute`：布尔值，是否将渲染后的 SQL 发送到 IDE 配置的数据库执行（默认 `false`）
  * `dryRun`：布尔值，当 `execute=true` 执行 DML（INSERT/UPDATE/DELETE）时，是否在执行后立即执行事务回滚（默认 `true`，防止产生脏数据）
  * `dataSource`：指定执行的目标数据源名称（可选，默认使用当前项目配置的数据源）
  * `maxRows`：查询返回的最大行数限制（默认 50，防止全表扫描）
  * `dbType`：SQL 方言类型，如 `mysql`, `postgresql`, `oracle`, `sqlserver`, `h2`（默认自动根据数据源探测）
  * `username` / `password`：可选的数据库账号密码覆盖（默认自动从 IDEA Database 配置中读取）
  * `projectPath`：项目路径，可选

**输出：**

* `status`：执行状态（`success` 或 `error`）
* `statementId`：语句 ID
* `statementType`：语句类型（`select`, `insert`, `update`, `delete`）
* `renderedSql`：根据参数与分支条件最终拼装出的完整 SQL 语句
* `parameters`：参数代入明细列表（包含占位符 token、属性名、代入值、是否外部提供等）
* `ifTests`：各动态分支的实际求值结果及来源（`ognl`、`explicit`、`allIfTestsTrue` 等）
* `syntax`：Druid 语法解析校验结果（`valid` 是否合法、`dialect` 方言、语法报错信息）
* `execution`：数据库执行结果（仅在 `execute: true` 时返回）：
  * `executed`：是否执行成功
  * `dataSource`：执行所用数据源
  * `executionTimeMs`：执行耗时（毫秒）
  * `rowCount` / `affectedRows`：查询返回行数 / DML 受影响行数
  * `isDryRunRolledBack`：事务是否已安全回滚
  * `columns`：返回的列名列表
  * `rows`：返回的数据行二维数组
* `warnings`：执行过程中的警告提示

```json
// 示例调用：在事务回滚模式下测试一条动态查询 SQL
{
  "xmlPath": "src/main/resources/mapper/UserMapper.xml",
  "statementId": "selectUsersByCondition",
  "params": {
    "status": 1,
    "roleId": 2
  },
  "execute": true,
  "dryRun": true
}
```

---

### 10. `list_tables` —— 获取数据库所有表名

**输入：**

* `projectPath`：项目路径，可选；只打开一个项目时可以不传

**输出：**

项目中所有数据源及每个数据源下的所有表名列表（含数据源名称及 JDBC URL）。

> 配合 `get_table_columns`，AI 可迅速浏览全库表清单并选择目标表生成 CRUD。

---

### 11. `get_mybatis_generator_profile` / `set_mybatis_generator_profile` —— 读取与配置代码生成 Profile

获取或保存当前项目代码生成规则（包括实体类/Mapper/XML的包名、源码目录、Service/Controller 开关、Lombok 开关、批量插入方法等），让 AI 在调用 `generate_crud` 时自动对齐项目现有的架构规范。
---

## 📦 配置方式

MyBatisCodeHelper-Pro 内置了 MCP HTTP 服务器（默认端口 `63340`）。

### 方式一：一键生成 `.mcp.json`（推荐）

在 IDEA 菜单栏点击：

```text
Tools
    └── MyBatisCodeHelper
            └── MCP Server
```

在弹出的 MCP 设置弹窗中，支持 **一键在项目根目录生成或更新 `.mcp.json`**。  
Claude Code、Cursor、Cline、Oh My Pi 等支持标准 MCP 的 AI 编码工具会自动发现并加载该配置。

生成的 `.mcp.json` 内容示例：

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

### 方式二：手动配置到 AI 客户端

将以下配置添加到支持 MCP 的 AI 编码助手（如 cc switch 或客户端全局 MCP 配置）中：

服务名称可以设置为 `MybatisMcp`：
```json
{
  "type": "http",
  "url": "http://127.0.0.1:63340/mcp"
}
```

> 该 MCP 服务由 IntelliJ IDEA 插件 **MyBatisCodeHelper-Pro** 提供，需要先安装插件并启动 IDE。

## 🚦 启动 MCP 服务

MyBatisCodeHelper-Pro 提供两种启动方式。

### 方式一（推荐）

```text
Tools
    └── MyBatisCodeHelper
            └── Start MCP Server
```

启动成功后，IDE 右下角会弹出提示。

---

### 方式二

```text
Settings / Preferences

Tools
    └── MyBatisCodeHelper
            └── MCP Server
                    └── Start
```

---

### 如何确认已启动

启动成功后，菜单项会由

```text
Start MCP Server
```

变为

```text
Stop MCP Server
```

说明服务已经运行，此时 AI 编码助手即可通过 MCP 与当前项目进行交互。

> MCP 服务依赖 IntelliJ IDEA 运行。关闭 IDE 后服务会自动停止，重新打开 IDE 后需要重新启动。

---

## 💡 推荐使用场景

| 场景            | 推荐工具                     |
| ------------- | ------------------------ |
| 快速定位 XML      | `find_mapper_xml`        |
| 根据 XML 找接口    | `find_mapper_interface`  |
| 列出数据库所有表    | `list_tables`            |
| 编写 SQL 前查看表结构 | `get_table_columns`      |
| 查看已有 SQL 列表   | `list_mapper_statements` |
| 查看项目数据源       | `list_data_sources`      |
| **校验 Mapper 语法与契约** | **`validate_mybatis_mapper`** |
| **动态 SQL 渲染/校验/安全执行** | **`run_mybatis_sql`** |
| 根据表生成 CRUD 代码 | `generate_crud`          |
| 生成 Mapper 测试用例    | `generate_mapper_testcase` |
| 查询/配置代码生成规范 | `get_mybatis_generator_profile` / `set_mybatis_generator_profile` |
---

## 📊 核心优势

1. **🎯 更准确** —— 基于 IntelliJ IDEA 索引定位 Mapper 与 XML，减少 AI 找错文件的概率。
2. **📉 更少上下文占用** —— 返回结构化数据，而不是整个 XML 文件。
3. **⚡ 更快响应** —— 无需搜索和解析大量项目文件。
4. **💰 更低 Token 消耗** —— 减少 XML、DDL 等无关内容的读取。
5. **📈 项目越大收益越明显** —— XML 越多、SQL 越复杂，MCP 的优势越明显。
