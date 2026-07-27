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

## 📦 配置方式

将以下配置添加到支持 MCP 的 AI 编码助手（如 cc switch）配置中：

名称可以设置为MybatisMcp
```json
{
  "type": "http",
  "url": "http://127.0.0.1:63340/mcp"
}
```

> 以上为示例配置。该 MCP 服务由 IntelliJ IDEA 插件 **MyBatisCodeHelper-Pro** 提供，需要先安装插件并启动 IDE。

---

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
| 编写 SQL 前查看表结构 | `get_table_columns`      |
| 查看已有 SQL      | `list_mapper_statements` |
| 查看项目数据源       | `list_data_sources`      |
| 根据表生成 CRUD 代码 | `generate_crud`          |
| 生成 Mapper 测试    | `generate_mapper_testcase` |

---

## 📊 核心优势

1. **🎯 更准确** —— 基于 IntelliJ IDEA 索引定位 Mapper 与 XML，减少 AI 找错文件的概率。
2. **📉 更少上下文占用** —— 返回结构化数据，而不是整个 XML 文件。
3. **⚡ 更快响应** —— 无需搜索和解析大量项目文件。
4. **💰 更低 Token 消耗** —— 减少 XML、DDL 等无关内容的读取。
5. **📈 项目越大收益越明显** —— XML 越多、SQL 越复杂，MCP 的优势越明显。
