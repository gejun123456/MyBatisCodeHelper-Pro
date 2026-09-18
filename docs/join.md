# 生成多表关联 Join (支持平铺 Join 与 JSON 聚合 Join)

当我们使用从数据库生成 CRUD 时，只能生成单表操作的 SQL。如果多张表之间存在关联关系，怎么做到自动生成，并且满足以下需求？
1. **多表字段同名不冲突**：两张表即使有相同名字的字段，也能正确重命名与映射。
2. **表结构变动联动同步**：表中添加、修改或删除字段后，重新生成 CRUD 时关联字段能自动刷新，无需手动改 XML。
3. **一键生成完整闭环代码**：自动生成接口方法、SQL 语句、ResultMap、扩展实体类及转换器，开发者只需调用即可。

插件提供了两种强大的关联生成模式：
- **传统平铺 Join (Flat Join)**：适用于一对一 (`OneToOne`) 及无需分页的一对多关联。
- **JSON 聚合 Join (JSON Join)**：**专为一对多 (`OneToMany`) 分页场景设计**，利用数据库原生 JSON 聚合函数彻底解决主表分页错乱问题！

---

## 一、传统平铺 Join (Flat Join)

### 1. 字段冲突处理与 Join_Column_List

在 MyBatis XML 中，若两张表关联时字段重名，直接 `<include refid="Base_Column_List"/>` 会产生字段覆盖。为此，插件在子表和主表生成带有别名的字段片段：

```xml
<sql id="Join_Column_List">
  <!--@mbg.generated-->
  a.id as a_id,
  a.user_id as a_user_id,
  a.delete as a_delete,
  a.mydate as a_mydate
</sql>

<resultMap id="JoinResultMap" type="com.codehelper.domain.A">
  <!--@mbg.generated-->
  <id column="a_id" property="id"/>
  <result column="a_user_id" property="userId"/>
  <result column="a_delete" property="delete"/>
  <result column="a_mydate" property="mydate"/>
</resultMap>
```

在字段前加上表名/别名前缀，就彻底避免了同名字段冲突。

### 2. 平铺 Join 的生成结果

以一对一关联为例，生成代码如下：

- **扩展实体类**：
```java
public class AWithB extends A {
    private B b;
    public B getB() {
        return b;
    }
    public void setB(B b) {
        this.b = b;
    }
}
```

- **ResultMap 继承并嵌套关联**：
```xml
<resultMap id="selectJoin" type="com.codehelper.domain.AWithB" extends="JoinResultMap">
  <association property="b" resultMap="com.codehelper.mapper.BMapper.JoinResultMap"/>
</resultMap>
```

- **SQL 语句**：
```xml
<select id="AJoinB" resultMap="selectJoin">
  select <include refid="Join_Column_List"/>,
  <include refid="com.codehelper.mapper.BMapper.Join_Column_List"/>
  from a join b on b.a_id = a.id
</select>
```

- **Mapper 接口方法**：
```java
List<AWithB> AJoinB();
```

---

## 二、全新功能：一对多 JSON 聚合 Join (JSON Join)

### 1. 为什么需要 JSON Join？（解决一对多分页痛点）

在传统的一对多平铺关联中，通常使用 `LEFT JOIN` + `<collection>` 映射：
```sql
select ... from user u left join user_order o on o.user_id = u.id
```
**严重缺陷——主表分页错乱**：
- 如果一个用户有 3 笔订单，数据库查询会产生 3 行数据（笛卡尔积膨胀）。
- 当使用 `PageHelper`、`MyBatis-Plus` 分页插件或直接写 `LIMIT 0, 10` 时，LIMIT 是在数据库结果集行数上执行的。
- 结果：**明明限制了 10 条，实际只返回了 3~4 个用户的数据**，甚至第 4 个用户的订单数据被截断到下一页，导致分页总数、页码、数据完全对不上！

### 2. JSON Join 的解决思路

插件提供的 **JSON Join** 采用**相关子查询（Correlated Subquery）+ 原生 JSON 聚合函数**：
- 在 SQL 查询主表列的同时，通过子查询将子表的全部多条记录聚合成一个 JSON 数组列（例如 `childJson`）。
- **主表查询结果集严格保持 1:1**：每 1 条主表记录只返回 1 行，行数绝不膨胀。
- **分页完美兼容**：配合 `LIMIT` / `PageHelper` / `MyBatis-Plus` 分页，分页条数精确对应主表行数！
- **自动映射为实体列表**：插件自动生成工业级 Jackson TypeHandler，查询出的 JSON 数组在 MyBatis 反序列化时直接转换为 `List<Child>`，业务调用毫无违和感。

---

## 三、JSON Join 支持的数据库方言与生成效果

插件支持当前主流的关系型数据库，自动根据项目数据源生成最佳语法：

### 1. MySQL (要求 5.7.22+ / 8.0+)
利用 `json_arrayagg` 和 `json_object`：
```xml
<select id="selectUserWithOrders" resultMap="selectUserWithOrdersResultMap">
  select <include refid="Join_Column_List"/>,
  (
    select coalesce(json_arrayagg(json_object(
      <include refid="com.example.mapper.UserOrderMapper.Json_Column_List"/>
    )), json_array())
    from user_order c
    where c.user_id = `user`.id
  ) as userOrderJson
  from `user`
</select>
```

### 2. PostgreSQL (要求 9.4+)
利用 `json_agg` 和 `json_build_object`：
```xml
<select id="selectUserWithOrders" resultMap="selectUserWithOrdersResultMap">
  select <include refid="Join_Column_List"/>,
  (
    select coalesce(json_agg(json_build_object(
      <include refid="com.example.mapper.UserOrderMapper.Json_Column_List"/>
    )), '[]')
    from user_order c
    where c.user_id = "user".id
  ) as userOrderJson
  from "user"
</select>
```

### 3. Oracle (要求 12c+ / 12.2+)
利用 `json_arrayagg` 和 `json_object`：
```xml
<select id="selectUserWithOrders" resultMap="selectUserWithOrdersResultMap">
  select <include refid="Join_Column_List"/>,
  (
    select nvl(json_arrayagg(json_object(
      <include refid="com.example.mapper.UserOrderMapper.Json_Column_List"/>
    )), '[]')
    from user_order c
    where c.user_id = "USER".id
  ) as userOrderJson
  from "USER"
</select>
```

### 4. SQL Server (要求 2016+)
利用 `FOR JSON PATH`：
```xml
<select id="selectUserWithOrders" resultMap="selectUserWithOrdersResultMap">
  select <include refid="Join_Column_List"/>,
  (
    select coalesce((
      select <include refid="com.example.mapper.UserOrderMapper.Json_Column_List"/>
      from user_order c
      where c.user_id = [user].id
      for json path, include_null_values
    ), '[]')
  ) as userOrderJson
  from [user]
</select>
```

---

## 四、子表字段维护：Json_Column_List 与 MBG 自动同步

为了支持表字段增删改后的自动维护，插件会在子表的 Mapper XML 中生成带有 `@mbg.generated` 标记的 `<sql id="Json_Column_List">`：

- **MySQL / PostgreSQL 格式**：
  ```xml
  <sql id="Json_Column_List">
    <!--@mbg.generated-->
    'id', c.id,
    'userId', c.user_id,
    'orderNo', c.order_no,
    'amount', c.amount,
    'createTime', c.create_time
  </sql>
  ```
- **Oracle 格式**：
  ```xml
  <sql id="Json_Column_List">
    <!--@mbg.generated-->
    'id' value c.id,
    'userId' value c.user_id,
    'orderNo' value c.order_no,
    'amount' value c.amount,
    'createTime' value c.create_time
  </sql>
  ```
- **SQL Server 格式**：
  ```xml
  <sql id="Json_Column_List">
    <!--@mbg.generated-->
    c.id as [id],
    c.user_id as [userId],
    c.order_no as [orderNo],
    c.amount as [amount],
    c.create_time as [createTime]
  </sql>
  ```

> **表结构变更自动刷新**：当你在子表新增或删除字段后，通过插件重新从数据库生成 CRUD 时，插件会自动识别并更新 `<sql id="Json_Column_List">`，无需手动去改动 JSON 字段拼接，保证永远与最新表结构一致！

---

## 五、自动生成的配套 Java 代码

### 1. 扩展实体类 (Domain Class)
继承主表实体，并包含子表列表字段：
```java
public class UserWithUserOrderJson extends User {
    private List<UserOrder> userOrderList;

    public List<UserOrder> getUserOrderList() {
        return userOrderList;
    }

    public void setUserOrderList(List<UserOrder> userOrderList) {
        this.userOrderList = userOrderList;
    }
}
```

### 2. 工业级通用 TypeHandler
自动在实体类同包目录下生成 `UserOrderListTypeHandler.java`：
- **深度时间兼容**：内置 `FLEXIBLE_DATE_FORMATTER`，支持纯日期（`yyyy-MM-dd`）、ISO 8601 标准、空格分隔格式、微秒/纳秒小数位、带时区偏移（`+HH:MM` / `Z`）以及时间戳，完美兼容 `Date`、`LocalDateTime`、`LocalDate`、`LocalTime`。
- **空安全兜底**：当 JSON 为空或子表无关联数据时，返回 `Collections.emptyList()`，杜绝业务调用出现 `NullPointerException`。
- **依赖说明**：基于 Jackson 实现（Spring Boot 工程默认已包含 `jackson-databind` 依赖，如为非 Spring Boot 工程请添加 Jackson 依赖）。

### 3. ResultMap 映射
```xml
<resultMap id="selectUserWithOrdersResultMap" type="com.example.domain.UserWithUserOrderJson" extends="JoinResultMap">
  <result property="userOrderList" column="userOrderJson" typeHandler="com.example.mapper.UserOrderListTypeHandler"/>
</resultMap>
```

### 4. Mapper 接口方法
```java
List<UserWithUserOrderJson> selectUserWithOrders();
```

---

## 六、使用步骤说明

1. **前提条件**：主表和子表已生成基础 CRUD，且主表 XML 中存在 `BaseResultMap`（带有表名识别信息）。
2. **触发动作**：在主表 Mapper XML 编辑器中，右键选择 **generateJoin**。
3. **配置 Statement**：
   - 填写 `ResultMap ID`（默认 `selectByJoinResultMap`）。
   - 填写 `Statement ID`（默认 `selectByJoin`）。
4. **添加关联关系**：点击右侧 **Add** 按钮，弹出 **Add RelationShip** 对话框：
   - **Relationship**：选择 **OneToMany**（一对多）。
   - **Xml file path**：输入或下拉选择子表 Mapper XML 文件（支持输入补全）。
   - **勾选「JSON 聚合(JSON Aggregation)」**：勾选后即可启用 JSON Join 模式。
   - **父表关联列 (Parent Join Column)**：下拉选择主表的关联列（例如 `id`）。
   - **子表关联列 (Child Join Column)**：下拉选择子表的关联列（例如 `user_id`）。
   - **数据库类型 (Database Type)**：选择当前数据库（MySQL / PostgreSQL / Oracle / SQL Server）。插件会自动根据数据源识别默认数据库，若手动选择与检测不一致会有提示。
5. **完成生成**：点击 OK 保存关系，再点击主对话框 OK，插件将自动完成全部代码生成！

---

## 七、平铺 Join 与 JSON 聚合 Join 选型对比

| 对比项 | 传统平铺 Join (Flat Join) | JSON 聚合 Join (JSON Join) |
| :--- | :--- | :--- |
| **推荐适用场景** | 一对一 (`OneToOne`)、无分页的小数据量一对多 | **一对多 (`OneToMany`)、有分页需求的主表关联** |
| **主表分页支持** | ❌ **不支持**（行数被子表放大，`LIMIT` 错乱） | ✅ **完美支持**（主表行数严格 1:1，分页精确） |
| **数据库版本** | 任意数据库均可 | MySQL 5.7.22+/8.0+, PostgreSQL 9.4+, Oracle 12c+, SQL Server 2016+ |
| **SQL 形式** | `LEFT JOIN ...` | 标量子查询 + `json_arrayagg` / `json_agg` / `for json` |
| **MyBatis 映射** | `<association>` / `<collection>` 嵌套映射 | 专属 Jackson `TypeHandler` 映射为 `List<T>` |
| **字段联动维护** | 重新生成 CRUD 自动更新 `Join_Column_List` | 重新生成 CRUD 自动更新 `Json_Column_List` |
| **网络传输冗余** | 子表多行时会重复传输主表所有字段 | 主表每条记录仅传输一次，子表数据打包为 JSON 字符串 |
