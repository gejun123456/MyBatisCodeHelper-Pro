2.0.0
- 识别mybatis的标签 如trim set where include， 提供在这些标签后的sql的自动补全 检测sql的正确性
- 可以通过数据库的表来生成java类
- 可以通过数据库的表来生成sql表中的所有字段
- 对 generatePageQuery提供更好的支持
- 支持 findByATrue  findByAFalse语法
- if test的自动补全 更好的支持
- 数据库生成crud时 提供实现Serializable接口
- 在< 或者<= 提供一键插入cdata

1.9.9
- 修复java类生成crud代码 需要忽略掉static字段
- 对mybatis的注解 提供sql补全功能
- 生成if test时 对于string 判断null和空
- 可以一键在mybatis 的resultMap上生成所有的property
1.9.8
- 数据库生成crud 支持java8的时间类型
- 直接从xml sql 生成java类和resultMap
- 修复部分用户激活时log4j的bug
1.9.5
- 修复 @MapperScan注解 spring没有注入的问题
- 更好的激活体验
1.9.4
- 数据库生成crud对多module的项目 支持更好
- 修复在module项目 一键生成testcase
- 设置界面可以插件激活码到期时间
1.9.3
- 可以通过方法名insertList, insertSelective来生成插入语句
- 修复可能的nullPointer

1.9.1 1.9.2
- 修复使用Intellij的数据库生成的默认类型
- 通过数据库生成时 包名可以自动提示

1.9.0
- 修复intellij重启后配置失效的bug

1.8.9
- 支持高清图标
- mybatis接口一键生成testcase 可对复杂的sql 快速进行测试 不需要要启动spring容器
- java生成crud代码支持postgresql
- 数据库生成时支持使用lombok 支持添加mapperscan注解 toString方法等
- 修复alt+enter在方法名生成sql时的thread报错
- 修复数据库生成时勾选列
1.8.8
- 加快mybatis接口和xml关联的速度
1.8.7
- 直接在Intellij的datasource中生成crud代码
- 添加resultMap property是否正确的检测
- sql中的param if test的自动补全的优化
- bug修复

1.8.6
- 添加2018.1及之后版本的spring支持
- 修复resultMap的自动补全
- 优化check resultMap的提示

1.8.4
- 使用数据库生成时可以自定义字段
- Intellij高级版支持 param的自动补全
- 添加spring的支持

1.8.3
- 离线激活支持
- 解绑支持
- 数据库界面优化

1.8.2
- 修复mysql使用mybatis generator生成时的数据库名


1.8.1
- 添加sqlserver和 oracle10g和 mysql8.0的支持
- 修复BaseColumnList重复生成的问题
- 支持mybatis上 insertProvider等注解


1.8.0
- 支持识别resultMap的extend属性
- 添加oracle和postgresql的支持
- mybatis generator的ui优化
- 自动import优化


1.7.7
- 可以直接从java类跳转到xml
- 一键为方法添加param注解
- 更新生成到mysql的编码为uft8mb4
- 修复findByLike


1.7.6
- 记忆用户保存的路径
- java和xml相互跳转添加快捷键
- 修复编码错误
- 可以配置使用project scope还是module scope
- 修复生成mybatis generator的xml
- 支持一个mapper对应多个xml

1.7.4
- 一键生成mybatis generator的xml文件
- 当更新java类的时候添加jdbcType
- 当xml不被使用时使用警告而不是标红

1.7.3
- 修复thread assertion报错
- 使用mybatis generator时不修改dao文件
- 修复java dateTime的jdbcType

1.7.2  
- 修复 html中 select标签报错  

1.7.1 
- 修复intellij 2017.3的报错
- 优化mac下的ui显示
- 修复orderby多个字段
- 通过数据库的表生成sql添加滚动条
- 不使用的xml标红，可以一键删除


1.7.0
- 生成service添加override注解
- 修复生成的service没有导入java包的问题
- 修复findFirstN没有返回List的问题


1.6.9
- 方法名自动生成增强
- 修复Long类型的jdbcType
- 支持transient字段类型
- findOne不再生成limit 1 可用findFirst


1.6.8
- 修复xml变动时图标会消失的问题
- 支持生成jdbcType

1.6.7
- 生成sql可从java类中生成注释
- 支持切换图标
- 支持updateIncVersion语法

1.6.5
- 支持findWithPage
- 支持自定义mapper后缀

1.6.4
- 支持sqlite
- oracel支持生成多字段唯一，多字段索引

1.6.0
- 支持查询条件加上if test
- 支持生成多字段索引和多字段唯一
- 支持生成方法 max,min,sum等方法
- 支持生成 findOne,Before,After等语法
- 当查找多个字段时支持生成DTO
- 支持生成接口和接口实现
- 生成的dao不再使用pojo作为param
- 修复byte类型的生成

1.4.2
- 支持oracle
- 配置使用useGenerateKey
- resultMap refid keyProperty if test的自动补全
- 支持java8 time里的类型
- 添加新图标
- 在通过方法名生成sql如果接口引入其他类型比如（java.util.Date)自动import到接口中
- bugfix 修复生成文件为null和initialize class com.ccnode.codegenerator.freemarker.TemplateUtil exception(大部分mac会出现的问题)

1.3
- 生成mybatis文件时可生成索引及选择是否需要默认值
- 生成mybatis文件加入insertSelective
- 在配置中可选择mybatis接口是否加上@Mapper注解
- 方法名生成sql 支持greaterThanOrEqualTo lessThanOrEqualTo betweenOrEqualto
- 支持resultMap refid跳转至定义及重构
- 支持xml中的方法名重构
- 修复module为空的警告


1.2
- 添加mapper与dao的相互跳转
- 使用alt+insert生成xml
- 添加方法名生成sql
- 添加方法名自动提示
