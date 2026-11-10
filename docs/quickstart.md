# 快速开始：让 AI 配合插件完成一次 MyBatis 修改

从一个已有 Mapper 开始，体验“读取上下文 → 修改 → 检查 → 验证”的流程。准备一个可以运行的 MyBatis 项目和开发 / 测试数据库；IDEA 需要保持打开，并完成项目索引。

## 1. 选择版本并安装

| 购买渠道 | 应安装的插件 | 试用与购买 |
| --- | --- | --- |
| brucege.com 官网 | MyBatisCodeHelperPro，不带 Marketplace Edition | [官网试用与购买](https://brucege.com/pay/view) |
| JetBrains Marketplace；企业客户及中国以外用户 | MyBatisCodeHelperPro (Marketplace Edition) | [Marketplace 页面](https://plugins.jetbrains.com/plugin/14522-mybatiscodehelperpro-marketplace-edition-) |

在 IDEA 的 **Settings / Preferences → Plugins → Marketplace** 搜索对应名称并安装，按 IDE 提示重启。两个发行版本的购买和激活渠道不同，请使用与你的授权对应的版本。

试用申请、价格与授权条件以对应购买页面为准。[查看安装、激活与解绑说明](install.md)。

## 2. 配置数据库

在 IDEA 的 Database 工具窗口连接项目使用的开发 / 测试数据库，确认能看到本次任务所需的表和字段。多数据源项目需要明确目标数据源和 schema。

[数据库配置说明](configure.md) · [社区版使用说明](community.md)

没有可用数据源时，部分项目检索与静态检查仍可使用，但不能把跳过的数据库检查当成通过。[查看校验范围](mcp.md)。

## 3. 启动 MCP 并连接 AI 客户端

在 IDEA 的 **Tools → MyBatisCodeHelper → Start MyBatis MCP Server** 启动服务。也可以在设置中搜索 MyBatisCodeHelper 的 MCP 配置页。

启动窗口会显示当前服务地址和接入说明，默认地址为 `http://127.0.0.1:63340/mcp`。端口被占用时，在设置中修改，并使用窗口显示的实际地址。

- 根据你使用的客户端，按窗口提示生成项目配置或添加 HTTP MCP 服务。
- 支持项目 `.mcp.json` 的客户端可以使用窗口中的生成按钮；不同客户端的配置位置并不相同。
- WorkBuddy 用户可使用“写入 WorkBuddy”按钮。其他客户端的接入方式见 [MCP 配置与客户端接入](mcp.md)。

在 AI 客户端确认 `mybatis` 服务已连接，并能看到 `find_mapper_xml`、`validate_mybatis_mapper` 等工具。只有配置文件生成成功，还不能说明客户端已连接。

## 4. 生成项目的 AI Skill

使用 `Tools → MyBatisCodeHelper → Generate MyBatis AI Skill (SKILL.md)`，或 MCP 窗口中的生成 Skill 按钮，选择正在使用的客户端。

支持此功能的版本可为 Claude Code、CodeBuddy、WorkBuddy 生成 Skill，为 Cursor 生成规则。它们会告诉 AI 如何读取表结构、使用项目生成配置，以及检查和验证 Mapper。按提示重载项目或重启客户端。

如果找不到该菜单，请先检查所安装版本的更新记录；也可以先使用下面的任务提示词。[查看生成文件与版本说明](mcp.md#生成-ai-skill)。

## 5. 交给 AI 一个实际任务

将以下提示词中的接口名和需求替换为你自己的项目内容：

```text
请使用 mybatis MCP，修改 com.example.mapper.UserMapper：
为现有列表查询添加可选的 status 条件，并保持原有返回值和排序行为。

1. 找到接口对应的 XML，查看已有语句和实际表字段；先确认 status 的类型及映射。
2. 根据项目已有风格修改接口和 XML，不改动无关语句。
3. 调用 validate_mybatis_mapper，修复发现的问题，列出 checksSkipped。
4. 对 status 未传、传入有效值、查无结果三种情况，先用 execute=false
   渲染 SQL 并检查参数和条件分支。
5. 如需执行 SQL，使用已确认的开发 / 测试数据源。
   如生成 Mapper 测试，请补充有效参数、测试数据和结果断言，
   检查连接与事务配置后再运行。
6. 汇报修改的文件、已执行的检查、实际测试结果和仍未验证的内容。
   不要把静态检查通过或测试代码生成成功表述为业务验证通过。
```

## 6. 检查这次任务的结果

完成后应能看到：

- 接口与 XML 的具体修改，以及使用的实际表字段。
- 静态检查结果，包含已执行和跳过的检查项。
- 不同输入下渲染的 SQL；实际执行过测试时，还应有执行结果及断言结果。

`execute=false` 只渲染与检查 SQL，不会连接数据库执行。`dryRun` 用于执行 DML 后请求事务回滚，不能当作隔离环境；真实执行请使用开发 / 测试数据库。

如果生成了测试骨架，先补充真实输入与断言，再运行。生成器默认测试配置可能自动提交写入，应检查连接与事务设置。[查看 Mapper 测试说明](quicktestsql.md)。

## 遇到问题

| 现象 | 下一步 |
| --- | --- |
| AI 看不到工具 | 确认 IDEA 内服务已启动，客户端已启用服务，实际端口与配置一致 |
| 找不到 Mapper 或 XML | 等待索引完成，确认项目、接口 namespace 与模块关系；见 [常见问题](question.md) |
| 看不到表或列，或 schema 检查被跳过 | 检查数据源、可见 schema 和 [解析范围](configure.md) |
| 工具提示授权校验失败 | 检查试用 / 激活状态以及安装的发行版本；见 [激活说明](install.md) |

暂时不接 AI 也可以使用 [数据库生成代码](databaseToCrud.md)、[SQL 补全与检查](complete.md) 和 [快速测试 Mapper](quicktestsql.md)。

[开始试用 / 查看价格](https://brucege.com/pay/view) · [企业客户购买](company.md) · [联系支持](contactMe.md)
