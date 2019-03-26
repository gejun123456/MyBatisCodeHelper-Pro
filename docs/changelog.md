   <strong>2.5</strong>
        <ul>
            <li>[NEW]一键从xml生成join语句</li>
            <li>[IMPROVE]更短的xml注释</li>
            <li>[IMPROVE]去除blob字段的判断</li>
            <li>[IMPROVE]数据库生成crud 可以生成service接口</li>
            <li>[NEW]支持updateByXXX语法</li>
            <li>[NEW]支持sqlServer生成建表语句 方法名生成sql</li>
            <li>[NEW]可以定制数据库生成的crud方法</li>
            <li>[IMPROVE]ui美化</li>
            <li>[FIX]null pointer exception ModuleRootManager</li>
            <li>[FIX]hashMap$Node cast exception</li>
            <li>[FIX]临时文件没有删除</li>
            <li>[NEW]可以配置是否自动折叠自动生成的方法</li>
            <li>[NEW]mybatis selectKey的自动补全</li>
        </ul>
 <strong>2.4</strong>
    <ul>
        <li>[IMPROVE]数据库直接生成java类支持lombok Serializable等</li>
        <li>[IMPROVE]生成testcase会自动配置好typeAlias</li>
        <li>[IMPROVE]支持 findAllByXXX 语法</li>
        <li>[IMPROVE]数据库生成crud可选不生成jdbcType</li>
        <li>[IMPROVE]mybatis 配置文件resource的跳转自动补全</li>
        <li>[FIX]java类跳转到selectProvider优先选择当前module跳转</li>
        <li>[IMPROVE]typeAlias性能优化</li>
        <li>[FIX]使用mybatis datasource选择java8 LocalDateTime不生效的bug</li>
        <li>[NEW]从数据库可以直接生成batchInsert batchUpdate等</li>
        <li>[IMPROVE]数据库生成curd时添加fileHeader 比如@author</li>
        <li>[IMPROVE]findByXXIn使用Collection作为参数类型替代List</li>
        <li>[IMPROVE]数据库重新生成时会保留java model类中的transient字段及其get set方法</li>
    </ul>
<strong>2.3</strong>
        <ul>
            <li>[IMPROVE]springboot typealias 支持</li>
            <li>[IMPROVE]xml上 resultMap resultType parameterType 等检测</li>
            <li>[IMPROVE]多个foreach标签内的param补全支持</li>
            <li>[IMPROVE]通过数据库生成service 重新生成时 会检测service是否存在 合并内容</li>
            <li>[IMPROVE]方法名生成sql 使用 update count delete 可以生成if test</li>
            <li>[IMPROVE]findByAll使用model类作为参数</li>
            <li>[IMPROVE]generate testcase可以使用Intellij的数据库来生成jdbc配置</li>
            <li>[NEW]数据库生成crud 添加 batchInsert, batchUpdate, InsertOnDuplicate方法</li>
            <li>[IMPROVE]支持相同namespace的多个xml通过方法名来生成sql</li>
            <li>[FIX]修复oracle下param自动补全的exception</li>
            <li>[IMPROVE]使用方法名生成sql的格式优化</li>
        </ul> 
<strong>2.1</strong>
        <ul>
            <li>[New]从xml的sql一键测试sql 支持动态sql的测试</li>
            <li>[IMPROVE]java类生成crud可以选择其他module的路径</li>
            <li>[IMPROVE]支持collection array等不带参数的自动补全</li>
            <li>[IMPROVE]数据库使用通用mapper和mybatisplus生成时转义数据库关键字</li>
            <li>[IMPROVE]通用方法名生成sql 支持以select query get modify remove等关键字开头</li>
            <li>[IMPROVE]set trim where 标签后面的第一个if test不再高亮<li>
        </ul>
<strong> 2.0.3 </strong>
        <ul>
            <li> [FIX]生成测试用例数据库url使用本地时区替换utc时区</li>
            <li> [NEW]使用mybatis generator进行多表生成</li>
            <li> [IMPROVE] tk mapper可以配置超类</li>
            <li> [NEW]使用mybatis生成器可以生成service类</li>
            <li> [IMPROVE]自动完成when语句和resultMap jdbcType /li>
            <li> [IMPROVE] resultMap和refId从其他mybatis文件提供自动补全</li>
            <li> [FIX]oracle使用tk mapper column注解注释使用单引号不识别</li>
            <li> [NEW]mybatis sql标签自动提示列名 且不再报错</li>
            <li> [NEW]resultMap column根据property值来进行自动补全</li>
            <li> [NEW]mybatis generator生成时可以在表名前面添加schema名称</li>
        </ul>
2.0.2
- oracle date类型使用timeStamp作为jdbcType
- 数据库生成crud支持生成到通用mapper和mybatisPlus
- 方法名生成sql支持通用mapper和mybatisPlus
- 修复IndexNotReadyException
- 修复可能的方法名生成sql的Exception
- 设置界面优化
- sql param自动补全 添加jdbcType
- 修复实体类的注释 * 的问题
- findByLike 现在会添加% 符号
- 修复ctrl+alt+b跳转时可能的exception
- 使用mybatisDatabase连接数据库表太多时 会卡顿的问题
- 使用cd 一键生成cdata co 一键生成collection语句

2.0.1
- 数据库生成crud后立刻跳转到mapper接口文件
- 数据库生成crud支持swagger
- 数据库生成crud的java类型可以自动补全
- 数据库生成crud自动给sql关键字添加转义
- 数据库生成crud自动检测generatedKey
- 使用注解 支持注解sql字符串的+
- 可以使用ctrl+alt+b 从接口方法跳转到xml


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
