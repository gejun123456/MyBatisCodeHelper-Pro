# Generate Multi-Table Join (Flat Join & JSON Aggregation Join)

When generating CRUD code from a database table, it only generates single-table operations. When multiple tables have relationships, how can we automatically generate join queries that meet the following requirements?
1. **No column name collision**: Even if two tables have columns with identical names, they should be disambiguated with column aliases.
2. **Seamless schema sync**: When columns are added, modified, or removed in the tables, re-generating CRUD should automatically update the join column fragments without manual XML edits.
3. **End-to-end code generation**: Automatically generate Mapper methods, SQL statements, ResultMaps, extended domain models, and TypeHandlers.

MyBatisCodeHelper-Pro provides two join modes:
- **Traditional Flat Join**: Suitable for `OneToOne` relationships and small `OneToMany` relationships without pagination.
- **JSON Aggregation Join (JSON Join)**: **Specifically designed for `OneToMany` pagination scenarios**, using native database JSON aggregation functions to completely eliminate the pagination count distortion caused by Cartesian products!

---

## 1. Traditional Flat Join

### 1. Column Conflict Handling and Join_Column_List

When joining multiple tables in MyBatis XML, columns with identical names will collide if you simply use `<include refid="Base_Column_List"/>`. The plugin generates prefixed column aliases in both the parent and child table XMLs:

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

Adding the table alias prefix prevents name collisions.

### 2. Generated Code for Flat Join

Taking a `OneToOne` relationship as an example:

- **Extended Domain Class**:
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

- **ResultMap**:
```xml
<resultMap id="selectJoin" type="com.codehelper.domain.AWithB" extends="JoinResultMap">
  <association property="b" resultMap="com.codehelper.mapper.BMapper.JoinResultMap"/>
</resultMap>
```

- **SQL Statement**:
```xml
<select id="AJoinB" resultMap="selectJoin">
  select <include refid="Join_Column_List"/>,
  <include refid="com.codehelper.mapper.BMapper.Join_Column_List"/>
  from a join b on b.a_id = a.id
</select>
```

- **Mapper Method**:
```java
List<AWithB> AJoinB();
```

---

## 2. JSON Aggregation Join (JSON Join)

### 1. Why JSON Join? (Solving One-to-Many Pagination Issues)

In traditional one-to-many flat joins using `LEFT JOIN` + `<collection>`:
```sql
select ... from user u left join user_order o on o.user_id = u.id
```
**Major Problem — Broken Pagination on Main Table**:
- If a user has 3 orders, the database query returns 3 rows (Cartesian product row expansion).
- When using pagination plugins like `PageHelper`, `MyBatis-Plus`, or native `LIMIT 0, 10`, the `LIMIT` operates on raw database rows, NOT parent entities.
- **Result**: You request 10 records, but receive only 3~4 users' data, and the last user's orders may be sliced across pages!

### 2. How JSON Join Solves This

**JSON Join** leverages **correlated subqueries with native database JSON aggregation functions**:
- While querying the main table, a correlated subquery aggregates all matching child rows into a single JSON array column (e.g. `userOrderJson`).
- **Main query result count remains strictly 1:1**: Exactly 1 database row per parent entity.
- **Perfect pagination compatibility**: Works seamlessly with `LIMIT`, `PageHelper`, and `MyBatis-Plus`.
- **Automatic mapping**: The plugin automatically generates an industrial-grade Jackson TypeHandler that deserializes the JSON array column directly into `List<Child>`.

---

## 3. Supported Database Dialects and Generated SQL

### 1. MySQL (5.7.22+ / 8.0+)
Uses `json_arrayagg` and `json_object`:
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

### 2. PostgreSQL (9.4+)
Uses `json_agg` and `json_build_object`:
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

### 3. Oracle (12c+ / 12.2+)
Uses `json_arrayagg` and `json_object`:
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

### 4. SQL Server (2016+)
Uses `FOR JSON PATH`:
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

## 4. Child Column Maintenance: Json_Column_List & Automatic MBG Sync

To maintain consistency when table columns change, the plugin creates an `@mbg.generated` `<sql id="Json_Column_List">` in the child table Mapper XML:

- **MySQL / PostgreSQL**:
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
- **Oracle**:
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
- **SQL Server**:
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

> **Automatic Sync on Schema Changes**: When you add, modify, or remove columns in the database table and regenerate CRUD using the plugin, it automatically detects and updates `<sql id="Json_Column_List">` without overwriting your custom code.

---

## 5. Generated Java Artifacts

### 1. Extended Domain Class
Inherits the parent domain entity and adds the child list:
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

### 2. Production-Grade Jackson TypeHandler
Generates `UserOrderListTypeHandler.java` in the domain package:
- **Flexible Date/Time Parsing**: Built-in `FLEXIBLE_DATE_FORMATTER` based on `DateTimeFormatterBuilder`, handling pure date strings (`yyyy-MM-dd`), ISO 8601, space-separated formats, fractional seconds, timezone offsets (`+HH:MM` / `Z`), and epoch timestamps. Supports `Date`, `LocalDateTime`, `LocalDate`, and `LocalTime`.
- **Null Safety**: Gracefully returns `Collections.emptyList()` when the JSON column is null or empty, preventing NPEs.
- **Dependency Note**: Requires `jackson-databind` (included by default in Spring Boot projects).

### 3. ResultMap Mapping
```xml
<resultMap id="selectUserWithOrdersResultMap" type="com.example.domain.UserWithUserOrderJson" extends="JoinResultMap">
  <result property="userOrderList" column="userOrderJson" typeHandler="com.example.mapper.UserOrderListTypeHandler"/>
</resultMap>
```

### 4. Mapper Interface Method
```java
List<UserWithUserOrderJson> selectUserWithOrders();
```

---

## 6. How to Use

1. **Prerequisite**: Parent and child tables have generated basic CRUD, and the parent XML contains a `BaseResultMap`.
2. **Open Action**: Right-click anywhere in the parent table Mapper XML editor and select **generateJoin**.
3. **Configure Statement**:
   - Set `ResultMap ID` (default: `selectByJoinResultMap`).
   - Set `Statement ID` (default: `selectByJoin`).
4. **Add Relationship**: Click **Add** to open the **Add RelationShip** dialog:
   - **Relationship**: Choose **OneToMany**.
   - **Xml file path**: Select the child table Mapper XML (auto-completion supported).
   - **Check "JSON Aggregation"**: Enables JSON Join mode.
   - **Parent Join Column**: Select parent table join column (e.g. `id`).
   - **Child Join Column**: Select child table join column (e.g. `user_id`).
   - **Database Type**: Choose database dialect (MySQL / PostgreSQL / Oracle / SQL Server). The plugin automatically detects the current project's database.
5. **Generate**: Click OK to save the relationship, then click OK on the main dialog to generate all artifacts!

---

## 7. Flat Join vs JSON Join Comparison

| Feature | Flat Join | JSON Aggregation Join |
| :--- | :--- | :--- |
| **Best For** | `OneToOne`, small `OneToMany` without pagination | **`OneToMany` with pagination requirements** |
| **Main Table Pagination** | ❌ **Broken** (Row count multiplied by child records) | ✅ **Fully Supported** (Strictly 1:1 row count) |
| **Database Requirements** | Any database | MySQL 5.7.22+, PostgreSQL 9.4+, Oracle 12c+, SQL Server 2016+ |
| **SQL Implementation** | `LEFT JOIN ...` | Correlated subquery + `json_arrayagg` / `json_agg` / `for json` |
| **MyBatis Mapping** | `<association>` / `<collection>` | Jackson `TypeHandler` mapping to `List<T>` |
| **Schema Sync** | Auto-updates `Join_Column_List` on MBG rerun | Auto-updates `Json_Column_List` on MBG rerun |
| **Network Payload** | Duplicates parent columns across all child rows | Parent columns sent once, child data packed as JSON string |
