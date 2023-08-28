## 快速测试mybatis的sql (插件原创功能)

当我们写完sql后，我们需要测试下sql是否符合预期，在填入各种参数后能否正常工作，尤其是对于复杂的sql。

一般我们测试可能是如下的代码:

![springTestCase](https://images.brucege.com/springtestCase.gif)

由于需要启动spring，当项目较大的时候启动速度很慢，有些项目的启动时间超过30秒。导致测试sql速度很慢，改下sql重新再测试等很花时间。


如果只是单独测试sql是否正确，没必要启动spring容器，mybatis可以直接定义配置文件进行启动,如下

![quickTestJavaMapper](https://images.brucege.com/quickTestJavaMapper.png)

配置文件
![quickTestConfiguration](https://images.brucege.com/quickTestConfiguration.png)

这样我们可以直接测试mybatis的sql而不需要启动spring

速度非常快 如下：

![testSpeed](https://images.brucege.com/quickTestNoSpring.gif)

基本上1，2秒钟就跑完了。 相比启动spring的测试效率提升很高。

插件可以自动生成测试的java类和配置文件，不需要手动去配置。

![generateTestcase](https://images.brucege.com/autoGenerateTestCase.gif)


另外插件还可以快速构造测试数据，从表里面的数据生成java构造bean语句，提升写测试的效率

![GenerateJavaSetterFromTableRow](https://images.brucege.com/GenerateJavaSetterFromTableRow.gif)


## 插件生成testcase的配置文件不包含用户配置的mybatis插件，如果想在testcase使用如Pagehelper等可在设置中配置(2.8.3)

![testCaseAdditionalConfig](https://images.brucege.com/testCaseAdditionalConfig.png)

配置例子:
```
 <plugins>
        <plugin interceptor="com.github.pagehelper.PageInterceptor">
        </plugin>
    </plugins>
```

或者修改Inteceptor，修改setUp方法加入interceptor即可
```java
SqlSessionFactory builder = new SqlSessionFactoryBuilder().build(UserMapperTest.class.getClassLoader().getResourceAsStream("mybatisTestConfiguration/UserMapperTestConfiguration.xml"));
        //you can use builder.openSession(false) to not commit to database
PageInterceptor interceptor = new PageInterceptor();
builder.getConfiguration().addInterceptor(interceptor);
mapper = builder.getConfiguration().getMapper(UserMapper.class, builder.openSession(true));
```


## 生成testcase支持mybatisplus

在生成的testcase中有一个setUp方法，将SqlSessionFactoryBuilder改成MybatisSqlSessionFactoryBuilder即可测试mybatisplus自带的一些方法

## mybatisplus添加分页插件和乐观锁插件
在test类可以修改setUpMybatisDatabase 如下

```
@org.junit.BeforeClass
    public static void setUpMybatisDatabase() {
        SqlSessionFactory builder = new MybatisSqlSessionFactoryBuilder().build(SymphonyClientMapperTest.class.getClassLoader().
                getResourceAsStream("mybatisTestConfiguration/SymphonyClientMapperTestConfiguration.xml"));
        final MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        interceptor.addInnerInterceptor(new OptimisticLockerInnerInterceptor());
        interceptor.addInnerInterceptor(new PaginationInnerInterceptor());
        builder.getConfiguration().addInterceptor(interceptor);
        //you can use builder.openSession(false) to not commit to database
        mapper = builder.getConfiguration().getMapper(SymphonyClientMapper.class, builder.openSession(true));
    }
```





