# MyBatisCodeHelper-Pro

[![Jetbrains Plugins](https://img.shields.io/jetbrains/plugin/v/9837-a8translate.svg)][plugin]
[![Downloads](https://img.shields.io/jetbrains/plugin/d/9837.svg?style=flat-square)][plugin]
[![加入QQ群](https://img.shields.io/badge/chat-QQ群-46BC99.svg?style=flat-square)](//shang.qq.com/wpa/qunwpa?idkey=6bc11bfe278fa0d1d0d6292fa010b1aa8ddadbfeb70ef893083d5ab800137c1a)


qq群：542735979（插件bug修复 最新版本及问题讨论）

介绍视频:https://www.bilibili.com/video/av23458308/

Intellij下Mybatis支持插件 

## 功能
- 从java类生成mybatis crud代码 建表语句 支持生成service，建表支持生成多字段的索引
- 添加一个数据库 从数据库生成crud代码 支持mysql oracle sqlserver postgresql 
- 直接从Intellij自带的数据库生成crud代码
- 通过方法名(不需要方法的返回值和参数 会自动推导出来)来生成sql 可以生成大部分单表操作的sql 只需要一个方法的名字即可 会自动补全好方法的参数和返回值 和springdatajpa的语句基本一致
- xml中的 param的自动提示 if test的自动提示 resultMap refid 等的自动提示
- xml中refid，resultMap等的跳转到定义
- mybatis接口和xml的互相跳转  支持一个mybatis接口对应多个xml
- 检测没有使用的xml 可一键删除
- 检测mybatis接口中方法是否有实现，没有则报红 可创建一个空的xml
- 检测resultmap的property是否有误 
- resultMap中的property的自动提示
- mybatis接口中一键添加param注解
- mybatis接口一键生成xml
- mybatis接口中的方法名重构支持
- 支持spring 将mapper注入到spring中 intellij的spring注入不再报错 支持springboot

-----------------------------------------------------------------------

可以免费试用: http://brucege.com/pay/view


不支持的功能
- 不支持生成关联表的sql (如果觉得可以实现可以联系我)

之后会加入更多功能

## 联系我


- 加入qq群  
542735979
![qqGroup](http://ogyxv3y5w.bkt.clouddn.com/qqgroup.png)


- 或者添加我的微信:

![weichaturl](http://ogyxv3y5w.bkt.clouddn.com/WechatIMG1.jpeg)


截图中的项目来自[https://github.com/gejun123456/codehelperPluginDemo](https://github.com/gejun123456/codehelperPluginDemo)

通过数据库来生成CRUD代码参考了 https://github.com/zouzg/mybatis-generator-gui 项目 已征得该项目作者同意


大家可以学习https://www.imooc.com/learn/924 来掌握更多使用Intellij的技巧 视频讲得很棒


[plugin]: https://plugins.jetbrains.com/plugin/9837





