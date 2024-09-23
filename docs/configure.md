## Intellij 高级版请配置好IDEA的自带的数据库 在mybatis中写sql时 sql会有检测以及大量的自动补全 提高效率

- 配置数据库  数据库名一定要填  数据库无法连接请切换驱动的版本
- 当库里面有多个schema时，每个schema都要配置一遍。比如 mysql localhost:3306 里面有多个库时，需要在idea配置多个，而不是一个选多个schema

![configureDatabase](https://images.brucege.com/configureDatabase.png)

- 配置当前项目对应的数据库类型(达梦数据库请配置为GenericSql字段便可自动提示,或者本地装一个oracle把表拷过去 这样一些函数也能自动提示) 另外mysql如果是mariadb一定要配置为mariadb

![databaseConfig](https://images.brucege.com/configDatabase.png)

- 配置插件方法名生成对应的数据库

![configPluginDatabase2](https://images.brucege.com/configPluginDatabase2.png)

- 使用 postgresql，oracle,sqlserver，或者多个数据库有相同表名时需要配置 resolution scope,解析范围

需要先反选 All，再选自己对应的库，或者按你的xml对应的文件夹路径来选择
![resolutionScope](https://images.brucege.com/resolutionScope.png)


## 配置好后的效果

![writeSql](https://images.brucege.com/writeSql.gif)
