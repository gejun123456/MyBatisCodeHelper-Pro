## mybatis param的自动补全
![betterParamAutoComplete](https://images.brucege.com/betterParamAutoComplete.gif)

## 根据 `parameterType` 补全 XML 参数（3.7.0 起）

如果 XML 语句没有对应的 Mapper 接口方法，插件会从 `parameterType` 的 Java 类全名或 [MyBatis 类型别名](typeAliasSupport.md) 推导参数类型。支持 `#{...}`、`${...}` 和 OGNL 中的嵌套属性，以及 `foreach` 的集合与元素、`bind` 的值和变量。

例如，若 `com.example.OrderFilter` 定义了 `customer.id` 和 `List<Long> orderIds`，以下语句即使只有 XML，也可以补全这些属性。

```xml
<select id="findOrders" parameterType="com.example.OrderFilter" resultType="long">
  SELECT id FROM orders
  <where>
    <if test="customer != null and customer.id != null">
      AND customer_id = #{customer.id}
    </if>
    <if test="orderIds != null and !orderIds.isEmpty()">
      AND id IN
      <foreach collection="orderIds" item="orderId" open="(" separator="," close=")">
        #{orderId}
      </foreach>
    </if>
  </where>
</select>
```

存在对应接口方法时，补全和检查仍以该方法的参数为准。对无法解析的参数或 OGNL 引用报错需要对应的接口方法。

## mybatis param检测是否正确
![检测param是否正确](https://images.brucege.com/检测param是否正确.gif)

## property refid resultMap等的自动补全
![autoCompleteForPropertyResultMapEct](https://images.brucege.com/autoCompleteForPropertyResultMapEct.gif)


## 任意位置的sql的自动补全 识别include trim where set 等mybatis的标签
对于Intellij的数据库来说 可以对一个xml的标签 注入sql语法
补全的时候由于不能识别mybatis的这些标签，导致在写了上述的标签后 之后的sql无法进行自动补全
插件优化了这块，可以让Intellij正确识别这些标签 正确解析sql语法

trim标签
![trim标签正确性检测](https://images.brucege.com/trim标签正确性检测.gif)

set标签
![set标签正确性](https://images.brucege.com/set标签正确性.gif)

解析sql的正确性 需要先配置下

![databaseConfig](https://images.brucege.com/configDatabase.png)





