# MyBatisCodeHelper-Pro

[![JetBrains Plugins](https://img.shields.io/jetbrains/plugin/v/9837-mybatiscodehelperpro.svg)](https://plugins.jetbrains.com/plugin/9837)
[![Downloads](https://img.shields.io/jetbrains/plugin/d/9837.svg?style=flat-square)](https://plugins.jetbrains.com/plugin/9837)

> **让 AI 写 MyBatis 少走弯路，节省开发时间与 Token。**

少找 XML、少复制表结构、少重复解释项目规范。MyBatisCodeHelper-Pro 将项目上下文、代码生成与检查工具接入你正在使用的 AI 编码助手，帮助减少整理信息和反复纠错的时间。

**[接入 AI，完成第一个任务](quickstart.md)** · **[免费试用 / 查看价格](https://brucege.com/pay/view)** · [企业客户购买](company.md) · [English](en/README.md)

## 时间和 Token 省在哪里？

| 重复工作 | 插件如何帮助 | 继续了解 |
| --- | --- | --- |
| 找 XML、复制表结构给 AI | 按需检索 Mapper、现有语句与真实字段，减少手动整理上下文的操作 | [AI 修改 Mapper 示例](ai-workflow.md) |
| 反复解释目录、包名和生成风格 | 读取项目生成配置，由工具生成实体、Mapper、XML 等重复代码 | [数据库生成代码](databaseToCrud.md) |
| 修改后反复对话、排查参数和映射错误 | 调用静态检查定位问题；按指定参数渲染动态 SQL，再针对问题修复 | [MCP 工具参考](mcp.md) |
| 为一个查询手动搭建测试骨架 | 生成无需启动 Spring 的 Mapper 测试骨架，补充参数和断言后运行 | [快速测试 Mapper](quicktestsql.md) |

通过 MCP，AI 可以直接调用这些能力；适合由工具完成的生成、检查和 SQL 求值步骤，也可以减少让模型反复推导和输出中间内容的需要。

**节省的是你的开发时间，以及不必要的 AI 消耗。** 按量计费时，更少的 Token 可能降低调用费用；固定订阅下，则主要帮助节约额度和时间。工具定义、调用和返回内容本身也占 Token，实际节省因任务、模型和客户端而异。[用同一任务比较效果](ai-workflow.md#如何比较时间与-token-消耗)。

## 从一个实际需求开始

例如：**给现有订单查询增加可选时间范围，保持原来的排序与返回结果。**

1. AI 通过插件定位 Mapper 与 XML，查询实际字段和类型。
2. 按项目已有风格修改接口和 SQL。
3. 调用静态检查，修复参数、映射或语法问题。
4. 用不同参数渲染动态 SQL；需要验证结果时，在开发 / 测试环境运行有明确断言的测试。
5. 汇报修改、实际执行的检查和仍未验证的内容。

[复制这个任务的提示词](ai-workflow.md) · [安装与连接 AI 客户端](quickstart.md)

**校验结果有明确范围：**静态检查通过表示已执行的检查未发现问题，应同时查看跳过项；SQL 渲染和测试代码生成也不等于业务验证通过。工具的实际使用条件见 [MCP 说明](mcp.md)。

## 把工作流程交给 AI

支持生成 AI Skill 的版本可为 Claude Code、CodeBuddy、WorkBuddy 生成 Skill，为 Cursor 生成规则，指导 AI 按“先读上下文、再修改、最后验证”的流程调用插件。

在 IDEA 中启动 **MyBatis MCP Server**，按窗口说明连接客户端，再生成对应 Skill。接入成功后，AI 客户端应能看到插件工具。

[一步步接入](quickstart.md) · [Skill 与客户端配置](mcp.md)

## 在 IDEA 中直接使用

无需接入 AI，也可以使用现有功能：

- [SQL 补全与检查](complete.md)、[接口与 XML 重构](refactor.md)、[ResultMap 支持](resultMap.md)。
- [方法名生成 SQL](methodNameToSql.md)、[SQL 转 Mapper](sqlToMybatis.md)、[生成 Join](join.md)。
- [数据库变更后增量生成](databaseToCrud.md)、[自定义模板](generateByTemplate.md)、[日志还原 SQL](sqlLog.md)。

![数据库生成代码演示](https://images.brucege.com/databaseCrud.gif)

[全部功能与免费 / 付费版对比](features.md) · [介绍视频](https://www.bilibili.com/video/av50632948)

## 选择版本，开始试用

| 你的购买渠道 | 安装版本 | 下一步 |
| --- | --- | --- |
| 官网购买 | MyBatisCodeHelperPro，不带 Marketplace Edition | [官网试用与价格](https://brucege.com/pay/view) |
| JetBrains Marketplace；企业客户及中国以外用户 | MyBatisCodeHelperPro (Marketplace Edition) | [Marketplace 试用与购买](https://plugins.jetbrains.com/plugin/14522-mybatiscodehelperpro-marketplace-edition-) |

两个发行版本的激活渠道不同。价格、试用及授权条件以对应购买页面为准；已有激活码请安装对应版本。

**[开始接入](quickstart.md)** · [安装、激活与解绑](install.md) · [常见问题](question.md) · [联系支持](contactMe.md)

[更新记录](changelog.md) · [项目致谢与演示项目](features.md)
