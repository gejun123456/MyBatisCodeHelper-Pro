# Features and Free / Pro Comparison

[Home](/en/README.md) · [MCP reference](/en/mcp.md) · [Try Marketplace Edition](https://plugins.jetbrains.com/plugin/14522-mybatiscodehelperpro-marketplace-edition-)

## Features
- **MyBatis MCP (Model Context Protocol) Support** — Provides 12 specialized MCP tools for Oh My Pi, Claude Code, Cursor, and other AI coding assistants (two-way mapper/XML navigation, table schema queries, CRUD and testcase generation, deep static contract validation `validate_mybatis_mapper`, dynamic SQL branch evaluation and safe dry-run execution `run_mybatis_sql`), with one-click `.mcp.json` generation

- **Generate SQL from method name** — just a method name, no params or return type needed. Works like Spring Data JPA
- **Full MyBatis SQL auto-complete** — recognizes MyBatis tags (`include`, `trim`, `set`, `where`, `foreach`), provides database-aware completion and correctness checks
- **Generate CRUD from database** — connect to IntelliJ's built-in database or add a connection, auto-detect `useGeneratedKey`, configure module folders automatically
- Convert SQL to MyBatis XML and Java interface methods
- Quick test MyBatis SQL with parameters
- MyBatis log to executable SQL
- Generate `CREATE TABLE` SQL from Java class
- Regenerate after DB changes using the generator merge rules; review generated markers and changes
- Jump between MyBatis interface and XML (supports one interface → multiple XMLs)
- Refactor interface method names (syncs with XML)
- Auto-complete for param, `if test`, `resultMap`, `refid`, `foreach`
- resultMap property auto-complete, inspection, and refactor (supports `collection`, `association`)
- resultMap column auto-complete and inspection
- Navigation to `refid` and `resultMap` definitions
- Detect unused XML files, delete with one click
- Detect interface methods without XML implementation
- Add `@Param` annotation with one click
- Generate XML from interface with one click
- Full `typeAlias` support
- `#{}` param inspection
- OGNL support (`if test`, `when test`, `foreach`, `bind`) — auto-complete, navigation, inspection
- Spring support — inject MyBatis mappers into Spring, Spring Boot compatible
- Generate TestCase for mapper methods — no Spring context needed, test complex SQL fast
- Generate JOIN queries
- Export resultMap and Java class from SQL
- XML code formatter

---

## Free vs Pro Features

The listed free features remain available without activation. The Pro version unlocks additional features. Trial and licensing terms are set by the purchase channel.

| Feature | Free | Pro |
|---------|:----:|:---:|
| Jump between interface & XML | ✔ | ✔ |
| Refactor method name | ✔ | ✔ |
| Add @Param one-click | ✔ | ✔ |
| Auto-complete (param, resultMap, refid) | ✔ | ✔ |
| resultMap property auto-complete | ✔ | ✔ |
| Detect unused XML | ✔ | ✔ |
| Detect unimplemented interface methods | ✔ | ✔ |
| resultMap property inspection | ✔ | ✔ |
| Spring injection support | ✔ | ✔ |
| Generate page query | ✔ | ✔ |
| Code templates (cdata, collection) | ✔ | ✔ |
| Add unused resultMap properties | ✔ | ✔ |
| **Generate TestCase** | ✘ | ✔ |
| **Method name to SQL** | ✘ | ✔ |
| **Generate CRUD from database** | ✘ | ✔ |
| **Java class to CREATE TABLE** | ✘ | ✔ |
| **collection param completion** | ✘ | ✔ |
| **SQL completion after MyBatis tags** | ✘ | ✔ |
| **#{} param inspection** | ✘ | ✔ |
| **OGNL support** | ✘ | ✔ |
| **param refactor** | ✘ | ✔ |
| **resultMap column inspection** | ✘ | ✔ |
| **XML code formatter** | ✘ | ✔ |
| **SQL to resultMap & Java class** | ✘ | ✔ |
| **SQL to MyBatis XML & method** | ✘ | ✔ |
| **Generate JOIN** | ✘ | ✔ |

Free trial: https://plugins.jetbrains.com/plugin/14522-mybatiscodehelperpro-marketplace-edition-

---

## Video

Introduction: https://www.bilibili.com/video/av50632948 (Chinese)

---

## Credits

This project uses or references the following projects:

- codehelper.generator: https://github.com/zhengjunbase/codehelper.generator
- mybatis: https://github.com/mybatis/mybatis-3
- mybatis generator: https://github.com/mybatis/generator
- pageHelper: https://github.com/pagehelper/Mybatis-PageHelper
- mybatis-generator-gui: https://github.com/zouzg/mybatis-generator-gui
- mybatis generator plugin: https://github.com/itfsw/mybatis-generator-plugin
- mybatisplus: https://github.com/baomidou/mybatis-plus
- batlog: https://github.com/PerccyKing/batslog

If you are the author of any of these projects, please contact me for a free permanent license key.

[plugin]: https://plugins.jetbrains.com/plugin/9837
