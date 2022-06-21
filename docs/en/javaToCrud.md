## Generate Create table sql by java class
![generateCreateTable](https://mybatis-1309801975.cos.ap-shanghai.myqcloud.com/screenshots/generateCreateTable.gif)

## how to use

- Use alt+insert on java class （generate mybatis files）to generate all filse（using ctrl+N on mac, the same shortcut for generate getter and setter)
- When your java class add field could also use alt+insert （generate mybatis files）to generate updated mapper sql)

## Rules

- java class generate files not support primitive type, so you need to change field type to Integer instead of int

Supported java class field types

| FieldType            |  Start support plugin version|
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
