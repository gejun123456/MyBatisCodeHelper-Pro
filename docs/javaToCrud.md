## 根据java对象一键生成建表语句
### 2.6版本已废弃掉java类生成crud功能，只支持java类生成建表sql语句，在创建完表后 从数据库进行生成，从数据库生成功能更多 数据库添加字段等更新也更方便

![generateCreateTable](https://images.brucege.com/generateCreateTable.gif)

## 使用方法

- 在java对象上使用alt+insert （generate mybatis files）生成对应的建表语句sql文件 （mac上使用 ctrl+N 即getter setter对应的快捷键)
## 注意的点

- java类生成文件这些 java类中的字段只支持对象类型 比如 int需要改写为Integer


现在支持的java对象字段类型

| 字段类型            |  开始支持的版本        |
|----------------------|-------------------  |
| java.lang.Integer    |   v1.2              |
| java.lang.Long       |   v1.2              |
| java.lang.FLoat      |   v1.2              |
| java.lang.Double     |   v1.2              |
| java.lang.Boolean    |   v1.2              |
| java.util.Date       |   v1.2              |
| java.lang.String     |   v1.2              |
| java.math.BigDecimal |   v1.2              |
| java.lang.Short      |   v1.2              |
|java.sql.Date | v1.3|
|java.sql.Time | v1.3|
|java.sql.Timestamp | v1.3|
|java.time.LocalDateTime | v1.3|
|java.time.LocalDate | v1.3|
|java.time.LocalTime | v1.3|
|java.time.OffsetDateTime | v1.3|
|java.time.OffsetTime | v1.3|
|java.time.ZonedDateTime | v1.3|
| java.lang.Byte       |   v1.6.0              |
