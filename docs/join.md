当我们使用从数据库生成crud时，只能生成单表操作的sql
如果两张表 有关联关系 我们怎么来做自动生成  并且能满足以下条件  
1. 两张表有相同的字段 也能生成  
2. 在表中添加或减少字段后 关联的字段也能增加和减少  
3. 生成接口方法 和 resultMap 用户只需要加参数 和关联条件就行

我们可以先观察下 数据库生成crud生成的代码

```
 <resultMap id="BaseResultMap" type="com.codehelper.domain.A">
    <!--@mbg.generated-->
    <id column="id" property="id" />
    <result column="user_id" property="userId" />
    <result column="delete" property="delete" />
    <result column="mydate" property="mydate" />
  </resultMap>
  <sql id="Base_Column_List">
    <!--@mbg.generated-->
    id, user_id, `delete`, mydate
  </sql>
```
会有一个BaseResultMap和一个BaseColumnList两个块   这个BaseResultMap和BaseColumnList在表字段变了后 也会相应变化
在mybatis的xml中 我们可以引用其他xml定义的resultMap和sql块 
我们写一个join的sql 可以是
```
 select
    <include refid="Base_Column_List" />,<include refid="com.codehelper.mapper.BMapper.Base_Column_List"/>
    from a join b on b.a_id = a.id
```
但是如果两张表有相同的字段的话 就会用不了 

字段冲突了 我们可以在字段前加一个表名  即下面这种
```
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
在前面加一个前缀 就不会有冲突了 

这时我们可以写出sql
```
 <select id="AJoinB" resultMap="selectJoin">
    select<include refid="Join_Column_List"/>,
    <include refid="com.codehelper.mapper.BMapper.Join_Column_List"/>
    from a join b on 
  </select>
```
对于两张表关联 可能是一对一 或者一对多

我们也可以生成好实体类   如果是 一对一的话  生成类为
```
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
xml中的resultMap也可以生成好

```
  <resultMap id="selectJoin" type="com.codehelper.domain.AWithB" extends="JoinResultMap">
    <association property="b" resultMap="com.codehelper.mapper.BMapper.JoinResultMap"/>
  </resultMap>
```
接口中的方法也可以自动生成好
```
List<AWithB> AJoinB();
```

对于 生成 的 join_column_list 和 joinResultMap 都在当前表的范围内 
当用户在表重新生成crud时 我们可以检测当前表是否存在 joinColumnList这个 如果有就给更新掉
这样可以保证在表添加修改减少字段时 都能更新掉

在这个生成之后 我们添加一下参数 和关联关系 就可以直接使用了

在xml编辑器里面右键选择 generateJoin 即可

最终生成截图 (2.7.6)
![multipleTableJoin](https://images.brucege.com/multipleTableJoin.gif)

使用该功能生成目前有一个要求 中需要有BaseResultMap存在，这样插件可以找到表名 (可以通过表上右键mybatis generator左下角预览xml弄到BaseResultMap带有表名)








