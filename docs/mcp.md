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
6. **动态 SQL 分析与免跑单测置信度评分（Confidence Scoring）：**
   - 自动识别 `<if>`, `<choose>`, `<when>`, `<otherwise>`, `<where>`, `<trim>`, `<set>`, `<foreach>`, `${...}` 动态标签
   - **置信度 1.0（纯静态 SQL）**：所有语句均为确定性纯静态 SQL 且通过全部契约校验，此时 AI 可确信该 SQL 100% 正确，**安全免跑单测**，极大节省测试与生成耗时
   - **置信度 0.7（包含动态 SQL 标签）**：静态契约校验通过，但因包含动态条件分支，提示 AI 使用 `run_mybatis_sql` 进行分支求值验证，或使用 `generate_mapper_testcase` 生成多分支单元测试
   - **置信度 0.0（存在错误）**：直接返回具体错误行号、错误描述和修复建议

**输入：**
- `mapper`：Mapper 接口全限定名（如 `com.example.mapper.UserMapper`）或 `.java` 文件路径（与 `xmlPath` 二选一）
- `xmlPath`：Mapper XML 文件路径（与 `mapper` 二选一）
- `statementId`：可选，指定单独校验某一条 statement ID；省略时校验当前 Mapper 中的所有 statement 与 resultMap
- `projectPath`：项目路径，可选（仅打开单一项目时可省略）

**输出：**
- `valid`：是否校验通过（`true` / `false`）
- `confidence`：契约置信度（`1.0` 纯静态免测 / `0.7` 动态分支推荐验证 / `0.0` 发现错误）
- `recommendation`：总体评估与下一步动作建议
- `summary`：统计信息（总语句数、静态语句数、动态语句数、总错误数、总警告数、动态 SQL 注意事项）
- `resultMaps`：各个 ResultMap 的详细校验结果（字段匹配、错误及警告列表）
- `statements`：各个 Statement 的详细校验结果（包含 `hasDynamicSql`、`dynamicTags`、`sqlSyntax`、错误及警告列表）
- `globalErrors` / `globalWarnings`：命名空间不匹配、未实现接口方法等全局契约问题

---

### 9. `run_mybatis_sql` —— 动态 SQL 求值渲染、语法校验与安全执行

提供**无需启动 Spring 容器或运行单测**的 Headless 动态 SQL 求值引擎，支持传参模拟、分支条件强制覆盖、Druid SQL 语法解析，以及连接真实数据库执行（支持事务自动回滚）。

**核心能力：**
- **动态 SQL 求值与渲染**：模拟 MyBatis 运行时求值逻辑，处理 `<if>`, `<choose>`, `<when>`, `<where>`, `<trim>`, `<set>`, `<foreach>`, `<bind>` 以及 `#{}` 参数替换与 `${}` 表达式拼接，渲染出真实可执行的标准 SQL。
- **分支覆盖与条件控制**：
  - 支持传入 `params`（如 `{"status": 1, "userId": 1001}`）自动进行 OGNL 求值
  - 支持传入 `ifTests` 精确覆盖特定 `<if test>` 条件（如 `{"status != null": true}`）
  - 支持 `allIfTestsTrue: true` 强制开启全部动态分支（快速验证全覆盖 SQL 语法）
  - 支持 `allIfTestsFalse: true` 强制关闭全部动态分支（验证基础 SQL 语法）
- **Druid SQL 语法解析**：使用内置 Druid 语法解析器针对目标方言（MySQL, PostgreSQL, Oracle, SQLServer, H2, DB2 等）进行静态语法校验，检测关键字拼写、逗号缺失、括号不闭合等语法错误。
- **真实数据库安全执行（带 dryRun 回滚）**：
  - 自动复用 IntelliJ Database 工具窗口已保存的连接凭据，也可传入 `username`/`password` 临时覆盖
  - 查询类语句（SELECT）受 `maxRows` 行数保护（默认 50 条），防止大表数据撑爆 AI 上下文
  - 更新类语句（INSERT/UPDATE/DELETE）默认开启 `dryRun: true`，在事务中执行后**自动回滚**，既能验证 SQL 在真实数据库能否正常执行，又绝不污染或破坏业务数据。
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

**Oh My Pi**、**Claude Code**、**Cursor** 等 AI 编码工具在打开该项目时会自动发现并连接该 MCP 服务。

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

#### 4. Codex / stdio 桥接（DeepSeek CLI / Python）

对于只支持 stdio 传输协议的客户端，可以通过 `mcp-remote` 将 HTTP 端点转为 stdio（例如在 `~/.codex/config.toml` 中）：

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
            └── Start MCP Server
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

| 场景 | 推荐工具 | 优势说明 |
| --- | --- | --- |
| 快速定位 XML | `find_mapper_xml` | 精准匹配，避免同名文件定位错误 |
| 根据 XML 找接口 | `find_mapper_interface` | 双向契约直达 |
| 编写 SQL 前查看表结构 | `get_table_columns` | 获取精准字段与 Java 映射类型 |
| 查看已有 SQL | `list_mapper_statements` | 无需读取大体积 XML，直接返回语句元数据 |
| 查看所有数据库表 | `list_tables` | 按数据源和 schema 列出全部表 |
| 查看项目数据源 | `list_data_sources` | 了解当前配置的数据库连接 |
| **静态校验 Mapper 与 XML 契约** | `validate_mybatis_mapper` | **深度检测属性映射、OGNL、参数绑定，标红语法错误** |
| **纯静态 SQL 免测判断** | `validate_mybatis_mapper` | **置信度 1.0 时安全免跑单测，省时省 token** |
| **动态 SQL 求值与渲染** | `run_mybatis_sql` | **模拟传参和 OGNL，零开销渲染最终 SQL** |
| **SQL 真实语法与分支覆盖** | `run_mybatis_sql` | **Druid 语法解析，一键全分支/基础分支测试** |
| **真实数据库安全执行** | `run_mybatis_sql` | **带 dryRun 事务回滚，验证真实 DB 执行且不污染数据** |
| 根据表生成 CRUD 代码 | `generate_crud` | 直接生成实体、Mapper、XML 及 Service |
| 生成 Mapper 单元测试 | `generate_mapper_testcase` | 自动配置 H2/真实库测试用例 |
| 读取代码生成规则 | `get_mybatis_generator_profile` | 获取包名、路径规范与代码风格 |
| 设置代码生成规则 | `set_mybatis_generator_profile` | 统一团队工程目录规范 |

---

## 📊 核心优势

1. **🎯 深度静态契约校验** —— 复用 IntelliJ IDEA 原生 DOM 与语言注入检查，识别 ResultMap 字段映射、OGNL 表达式语法、`#{}` 参数绑定及 XML 语法错误，纯静态 SQL 免跑单测（置信度 1.0）。
2. **⚡ Headless 动态 SQL 求值与安全执行** —— 无需启动耗时的 Spring 容器，直接求值 `<if>`/`<choose>` 等动态分支，Druid 语法解析，支持 DML 事务自动回滚（dryRun）。
3. **📉 极致减少上下文占用** —— 返回结构化数据，避免 AI 读取动辄几千 Tokens 的完整 XML 和 DDL。
4. **🛠️ 完善的生成与工程规范闭环** —— 支持读写工程代码生成配置（Profile），一键生成 CRUD 代码与单元测试。
5. **🔌 开箱即用的多客户端生态** —— 支持一键生成 `.mcp.json`，无缝对接 Oh My Pi、Claude Code、Cursor、Windsurf、Codex 等主流 AI 工具。
