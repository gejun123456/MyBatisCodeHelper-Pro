# Intellij Plugin for Mybatis

[![Jetbrains Plugins](https://img.shields.io/jetbrains/plugin/v/9837-a8translate.svg)][plugin]
[![Downloads](https://img.shields.io/jetbrains/plugin/d/9837.svg?style=flat-square)][plugin]
[![加入QQ群](https://img.shields.io/badge/chat-QQ群-46BC99.svg?style=flat-square)](//shang.qq.com/wpa/qunwpa?idkey=6bc11bfe278fa0d1d0d6292fa010b1aa8ddadbfeb70ef893083d5ab800137c1a)


<div align="left">
<a href="https://gejun123456.github.io/MyBatisCodeHelper-Pro/#/en/">English</a>
</div>
 &nbsp;&nbsp;

> Intellij下Mybatis支持插件 

qq群：542735979（插件bug修复 最新版本及问题讨论）

介绍视频:https://www.bilibili.com/video/av23458308/

文档地址： https://gejun123456.github.io/MyBatisCodeHelper-Pro/

## 功能
- **通过方法名(不需要方法的返回值和参数 会自动推导出来)来生成sql 可以生成大部分单表操作的sql 只需要一个方法的名字即可 会自动补全好方法的参数和返回值 和springdatajpa的语句基本一致**
- **sql全自动提示，sql正确性检测，插件会识别mybatis的一系列标签 如 include trim set where，在这些标签之后的sql可以自动提示数据库的字段，检测sql的正确性，从此不用担心sql写错**
- **直接从Intellij自带的数据库或者配置一个数据库生成crud代码 自动检测好 useGeneratedkey 自动配置好模块的文件夹 只用添加包名就可以生成代码了**
- 从java类生成mybatis crud代码 建表语句 支持生成service，建表支持生成多字段的索引
- 数据库添加字段后可以继续生成，不会修改之前已经在接口或xml添加的自定义的方法 无需再去进行手动的添加
- mybatis接口和xml的互相跳转  支持一个mybatis接口对应多个xml
- mybatis接口中的方法名重构支持
- xml中的 param的自动提示 if test的自动提示 resultMap refid 等的自动提示
- resultMap中的property的自动提示
- xml中refid，resultMap等的跳转到定义
- 检测没有使用的xml 可一键删除
- 检测mybatis接口中方法是否有实现，没有则报红 可创建一个空的xml
- 检测resultmap的property是否有误 
- mybatis接口中一键添加param注解
- mybatis接口一键生成xml
- 支持spring 将mapper注入到spring中 intellij的spring注入不再报错 支持springboot
- 一键生成mybatis接口的testcase 无需启动spring，复杂sql可进行快速测试

-----------------------------------------------------------------------

可以免费试用: http://brucege.com/pay/view

大家可以学习https://www.imooc.com/learn/924 来掌握更多使用Intellij的技巧 视频讲得很棒

该项目使用了或参考了以下项目:

mybatis：https://github.com/mybatis/mybatis-3

mybatis generator: https://github.com/mybatis/generator

pageHelper: https://github.com/pagehelper/Mybatis-PageHelper

mybatis-generator-gui: https://github.com/zouzg/mybatis-generator-gui

mybatis generator plugin: https://github.com/itfsw/mybatis-generator-plugin

如果您是这些项目的作者，请联系我，我将发送免费的永久key给您

[plugin]: https://plugins.jetbrains.com/plugin/9837





