## 从数据库同步已有 Java 实体与 Mapper XML（3.7.0 起）

数据库表新增列后，可以给已有的 Java 实体和 Mapper XML 补充字段与映射。先确认 Mapper XML 有 `resultMap`，且 `resultMap` 的类型能解析到 Java 实体。

1. 在 Mapper XML 编辑器中右键，选择 **从数据库同步实体与 XML…**，按提示选择 `resultMap`，再选择数据源并确认目标表。XML 入口支持插件配置的 JDBC 数据源和 IDEA 的 Database 数据源。
2. 也可以在 IDEA 的 **Database** 工具窗口中右键单张表，选择同一操作，再确认要同步的 Mapper XML 和 `resultMap`。
3. 勾选需要补充的列，点击 **对比修改…**，逐项查看 Java 属性、`resultMap` 和 SQL 的差异。
4. 根据需要勾选受支持的 `INSERT`、`UPDATE` 和自定义查询改动，点击 **应用所选修改** 写入文件。

同步会保留已有的 Java 类型和映射。构造器映射、嵌套属性映射或无法安全修改的 SQL 请手动处理。

## 使用Intellij自带的datasource来生成 最简单的从数据库生成代码

![intellijDatasourceGenerateCrud](https://images.brucege.com/databaseCrud.gif)

选定了module后 插件会自动配置好java model folder, java mapper folder 以及 resource folder 一般不需要修改

* 注意最后生成的路径都是folder+package  所以一般选定了module后 只用填package就行了

只用第一次使用配置好包名就行了，包名有自动补全 2.0.1版本后插件会自动检测 generatedKey 一般不需要配置

在数据库添加了字段后 也可以重新生成，并且不会覆盖你的mapper接口中已经添加的方法

可生成service 生成到通用mapper及mybatisplus

## 支持定制列 配置column和java映射关系，typeHandler配置
![customizedColumns](https://images.brucege.com/customizedColumns.png)


## 支持配置typemapper 配置表字段类型与java类型的映射关系
![typeMappSettins](https://images.brucege.com/typeMapperSettings.png)




## 代码是如何自动合并的
- mapper接口 如果新生成的接口中的方法包含原来接口中的方法会进行替换 即不会覆盖掉自己写的方法
- mapper xml 文件 首先会删除掉 @mbg generated 注释的方法 然后生成你选择的方法  即不会覆盖掉你自己写的方法
- java 实体 会保留java实体中的 static方法 static 字段 transient方法 transient字段
- 请不要修改自动生成的方法 如果要修改 请将sql中的 @mbg generated注释给去掉 以免在添加字段重新生成后 将该方法给覆盖掉了
- model类可以在设置里面关掉auto merge 以防添加字段后model类被覆盖(比如model添加了一些自定义的注解如jackson时)
- 请不要修改自动生成的xml语句，如果要改的话请使用一个新的id并去除掉注释，这样加字段生成的时候不会覆盖掉你的修改

## IDEA社区版可以使用添加的datasource来生成 （目前支持mysql oracle postgresql sqlserver  myql支持5.5及以上  oracle支持oracle10g及以上 postgresql sqlserver支持最新版，老版本未测试 有问题请联系我) 

![mybatis-database-generator](https://images.brucege.com/configDatabaseToUseMybatisGenerator.gif)

## 如何配置

一般只用配置下包名 就可以使用了
![mybatis-database-generator](https://images.brucege.com/DatabaseGenerateSetting.png)

### 什么时候需要清理表缓存
当你之前修改过定制列里面的java类型，之后又想变成插件自动转换的，或者你之前使用了
typeMapper后不想用了，或者你之前改了model名字都可以清理表缓存将这些重置为插件默认的  

### 使用java8 LocalDateTime
可以在设置中->other->MybatisCodeHelper  useJava8LocalDateTime勾一下就行 

