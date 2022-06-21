## Intellij 高级版请配置好IDEA的自带的数据库 在mybatis中写sql时 sql会有检测以及大量的自动补全 提高效率

- 配置数据库  数据库名一定要填  数据库无法连接请切换驱动的版本
- 当库里面有多个schema时，每个schema都要配置一遍。比如 mysql localhost:3306 里面有多个库时，需要在idea配置多个，而不是一个选多个schema 
![configureDatabase](https://mybatis-1309801975.cos.ap-shanghai.myqcloud.com/screenshots/configureDatabase.png)

- 配置当前项目对应的数据库类型(达梦数据库请配置为GenericSql字段便可自动提示,或者本地装一个oracle把表拷过去 这样一些函数也能自动提示) 另外mysql如果是mariadb一定要配置为mariadb
![databaseConfig](https://mybatis-1309801975.cos.ap-shanghai.myqcloud.com/screenshots/configDatabase.png)

- 配置插件方法名生成对应的数据库
![configPluginDatabase2](https://mybatis-1309801975.cos.ap-shanghai.myqcloud.com/screenshots/configPluginDatabase2.png)

- 如果有多个数据库，并且有相同的表名需要配置
![resolutionScope](https://mybatis-1309801975.cos.ap-shanghai.myqcloud.com/screenshots/resolutionScope.png)


## 配置好后的效果

![writeSql](https://mybatis-1309801975.cos.ap-shanghai.myqcloud.com/screenshots/writeSql.gif)
