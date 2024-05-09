# Intellij Plugin for Mybatis

[![Jetbrains Plugins](https://img.shields.io/jetbrains/plugin/v/9837-a8translate.svg)][plugin]
[![Downloads](https://img.shields.io/jetbrains/plugin/d/9837.svg?style=flat-square)][plugin]
[![加入QQ群](https://img.shields.io/badge/qq4群-46BC99.svg?style=flat-square)](https://qm.qq.com/cgi-bin/qm/qr?k=RGT8lzQMq-BAVQoV8Gcmj2ze9AjvMiEP&jump_from=webapi&authKey=xxoZFYvl6MHgatxT+DvJ0KjK3yLcQYpVqbjufgmWl6UKg55QCc9KZCC98y+YXSTl)


<div align="left">
<a href="https://gejun123456.github.io/MyBatisCodeHelper-Pro/#/en/">English</a>
</div>
 &nbsp;&nbsp;

> Intellij下Mybatis支持插件 

qq群（插件bug修复 最新版本及问题讨论）  
2群: 914051156 (人满)
3群：598080979 (人满)
4群：232578741 (人满)
5群: 575733084
1群备份: 789681969  
添加qq号:1098632410


介绍视频: https://www.bilibili.com/video/av50632948

文档地址： https://gejun123456.github.io/MyBatisCodeHelper-Pro/

国内文档地址：https://brucege.com/doc/#/

## 功能
- **通过方法名(不需要方法的返回值和参数 会自动推导出来)来生成sql 可以生成大部分单表操作的sql 只需要一个方法的名字即可 会自动补全好方法的参数和返回值 和springdatajpa的语句基本一致**
- **xml sql几乎所有地方都有自动提示，sql正确性检测，插件会识别mybatis的一系列标签 如 include trim set where，在这些标签之后的sql可以自动提示数据库的字段，检测sql的正确性，从此不用担心sql写错**
- **直接从Intellij自带的数据库或者配置一个数据库生成crud代码 自动检测好 useGeneratedkey 自动配置好模块的文件夹 只用添加包名就可以生成代码了**
- 从java类生成建表语句
- 数据库添加字段后可以继续生成，不会修改之前已经在接口或xml添加的自定义的方法 无需再去进行手动的添加
- mybatis接口和xml的互相跳转  支持一个mybatis接口对应多个xml
- mybatis接口中的方法名重构支持
- xml中的 param的自动提示 if test的自动提示 resultMap refid 等的自动提示
- resultMap中的property的自动提示
- xml中refid，resultMap等的跳转到定义
- 检测没有使用的xml 可一键删除
- 检测mybatis接口中方法是否有实现，没有则报红 可创建一个空的xml
- 检测resultmap的property是否有误
- param检测 检测#{ 中的内容是否有误
- ognl 支持 if test when test foreach bind中的自动补全，跳转和检测
- mybatis接口中一键添加param注解
- mybatis接口一键生成xml
- 完整的typeAlias支持
- 支持spring 将mapper注入到spring中 intellij的spring注入不再报错 支持springboot
- 一键生成mybatis接口的testcase 无需启动spring，复杂sql可进行快速测试
- 一键生成关联的join
- 一键从sql语句中 导出resultMap


-----------------------------------------------------------------------

## 插件未激活与激活状态的功能比较  未激活版的功能可以免费一直使用下去

功能点  |  未激活版 | 激活版
-----   | ------ | -----
接口与xml互相跳转 更换图标|  ✔ | ✔
接口方法名重构| ✔| ✔
一键添加param| ✔| ✔
xml中的 param的自动提示 resultMap refid 等的自动提示|✔| ✔
resultMap中的property的自动提示|✔|✔
检测没有使用的xml 可一键删除|✔|✔
检测mybatis接口中方法是否有实现，没有则报红 可创建一个空的xml方法块|✔|✔
检测resultmap的property是否有误|✔|✔
支持spring 将mapper注入到spring中 intellij的spring注入不再报错 支持springboot|✔|✔
一键生成分页查询|✔|✔
一键添加resultMap中未被使用的属性| ✔|✔
一键生成mybatis接口的testcase |✘|✔
通过方法名生成sql | ✘| ✔
通过数据库生成crud代码| ✘|✔
通过java类生成建表语句|✘|✔
xml collection中的 param提示| ✘|✔
识别mybatis的trim where include等标签 全自动sql补全| ✘|✔
检测#{中的参数是否正确| ✘|✔
if test when test foreach collection $中的OGNL支持| ✘|✔
param重构功能(2.7.2)| ✘|✔
resultMap中column提示与检测(2.7.2)| ✘|✔
Mybatis xml代码格式化(2.8.2)| ✘|✔
从sql生成resultMap和java类 | ✘|✔
从sql直接生成mybatis xml和java接口方法 | ✘    |✔

可以免费试用: http://brucege.com/pay/view

大家可以学习https://www.imooc.com/learn/924 来掌握更多使用Intellij的技巧 视频讲得很棒

该项目使用了或参考了以下项目:


codehelper.generator: https://github.com/zhengjunbase/codehelper.generator

mybatis：https://github.com/mybatis/mybatis-3

mybatis generator: https://github.com/mybatis/generator

pageHelper: https://github.com/pagehelper/Mybatis-PageHelper

mybatis-generator-gui: https://github.com/zouzg/mybatis-generator-gui

mybatis generator plugin: https://github.com/itfsw/mybatis-generator-plugin

mybatisplus: https://github.com/baomidou/mybatis-plus

batlog: https://github.com/PerccyKing/batslog

如果您是这些项目的作者，请联系我，我将发送免费的永久key给您

[plugin]: https://plugins.jetbrains.com/plugin/9837





