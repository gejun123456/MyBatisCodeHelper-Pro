# MyBatisCodeHelper-Pro

[![Jetbrains Plugins](https://img.shields.io/jetbrains/plugin/v/9837-mybatiscodehelperpro.svg)][plugin]
[![Downloads](https://img.shields.io/jetbrains/plugin/d/9837.svg?style=flat-square)][plugin]

> The MyBatis plugin for IntelliJ IDEA — works great alongside AI coding tools.

Gitter: https://gitter.im/MyBatisCodeHelper/Lobby

---

### 💡 Still need a MyBatis plugin in the AI era?

AI coding assistants are great at writing general logic, but MyBatis has specific needs that generic AI tools don't fully address:

| Scenario | AI Assistant | This Plugin |
|----------|-------------|-------------|
| **Generate CRUD** | Wait seconds, pay per token | Instant, one-time purchase |
| **Regenerate after DB change** | Re-prompt with full context | One-click, preserves your custom code |
| **Database-aware completion** | May hallucinate non-existent tables | Connects your real DB, 100% accurate |
| **SQL correctness check** | AI doesn't verify as you type | Real-time inspection, highlight errors immediately |
| **Cost** | $10-20/month or pay-per-token | Starts at $20/year, far cheaper |

**Best practice:** Use AI for business logic, use this plugin for MyBatis code correctness and productivity — they complement each other.

---

## Features

- **Generate SQL from method name** — just a method name, no params or return type needed. Works like Spring Data JPA
- **Full MyBatis SQL auto-complete** — recognizes MyBatis tags (`include`, `trim`, `set`, `where`, `foreach`), provides database-aware completion and correctness checks
- **Generate CRUD from database** — connect to IntelliJ's built-in database or add a connection, auto-detect `useGeneratedKey`, configure module folders automatically
- Convert SQL to MyBatis XML and Java interface methods
- Quick test MyBatis SQL with parameters
- MyBatis log to executable SQL
- Generate `CREATE TABLE` SQL from Java class
- Regenerate after DB changes without overwriting custom code
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

The free version is fully functional for daily use. The Pro version unlocks advanced features.

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