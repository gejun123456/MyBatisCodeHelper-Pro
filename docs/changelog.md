<strong>3.2.9</strong>
<ul>
<li>[IMPROVE]kotlin报错优化</li>
<li>[IMPROVE]支持mybatis ognl单个参数可以使用任意名字引用</li>
<li>[IMPROVE]提供界面来合并xml代码</li>
<li>[FIX]select中的column包含点号时添加到java类中报错优化</li>
</ul>
<ul>
<li>[IMPROVE]kotlin exception fix</li>
<li>[IMPROVE]support ognl use any name for single parameter</li>
<li>[IMPROVE]provide ui to merge xml</li>
<li>[FIX]select column with dot exception fix</li>
</ul>
<strong>3.2.8</strong>
<ul>
<li>[IMPROVE]性能优化，当有大量xml，在创建对应方法的xml后方法没有取消标红问题</li>
<li>[FIX]2023.3 当查询为select *时 resultMap column的提示和检测</li>
<li>[FIX]使用kotlin时select字段检测优化</li>
<li>[FIX]java接口方法返回值类型检测可能出现的null pointer exception</li>
<li>[IMPROVE]使用Autowire注解替代Resource注解</li>
</ul>
<ul>
<li>[IMPROVE]performance improvement when contain many xml</li>
<li>[IMPROVE]for 2023.3 version, when select *, resultMap column inspection and auto completion support</li>
<li>[FIX]select column inspection when resultType is from kotlin</li>
<li>[FIX]java method return type inspection null pointer</li>
<li>[IMPROVE]use autowire to replace resource annotation</li>
</ul>
<strong>3.2.6</strong>
<ul>
<li>[IMPROVE]从sql生成java接口方法的参数会根据字段类型来做判断</li>
<li>[IMPROVE]java接口方法返回值类型和xml resultType或resultMap不一致时可以快速修复java接口方法返回值类型</li>
<li>[FIX]从xml生成java类和resultMap报错优化</li>
<li>[FIX]支持kotlin接口参数为List类型的解析，支持泛型? extends解析</li>
<li>[FIX]select中查询字段检测优化了resultMap中使用columnPrefix的检测</li>
<li>[NEW]可以快速添加typeMapper,根据表中未匹配的字段来快速添加</li>
</ul>
<ul>
<li>[IMPROVE]from sql generate mybatis java method param type will based on query column type</li>
<li>[IMPROVE]provide auto fix on java method return type when java method return type is different to xml resultType or resultmap type</li>
<li>[FIX]fix exception when use xml generate java class and resultMap</li>
<li>[FIX]support param completion and inspection when method is using kotlin with List parameter, support ? extend as well</li>
<li>[FIX]select query column inspection will work when resultmap contains columnPrefix</li>
<li>[NEW]add typeMapper quicker when table has unmapped columns</li>
</ul>
<strong>3.2.5</strong>
<ul>
<li>[IMPROVE]可以从resultmap type快速配置typealias</li>
<li>[NEW]从sql快速生成mybatis的java接口方法和xml</li>
<li>[NEW]从#{}快速生成if test语句</li>
<li>[FIX]兼容2023.3 eap版本</li>
<li>[FIX]修复InvalidElementAccessException</li>
<li>[IMPROVE]快速修复java接口方法返回类型和xml返回类型不一致</li>
</ul>
<ul>
<li>[IMPROVE]config typeAlias when resultMap type is not found</li>
<li>[NEW]from sql generate mybatis method and xml, replace value to #{}</li>
<li>[NEW]add if test for #{}</li>
<li>[FIX]compatability for 2023.3 eap version</li>
<li>[FIX]fix InvalidElementAccessException</li>
<li>[IMPROVE]quick fix for java method return type different from xml return type</li>
</ul>
<strong>3.2.4</strong>
<ul>
<li>[IMPROVE]check resultMap columns支持更复杂的resultmap检测</li>
<li>[FIX]用户禁用了kotlin插件导致的#{}没有代码提示</li>
<li>[IMPROVE]支持idea社区版在xml上填入参数预览sql</li>
<li>[IMPROVE]使用convertTextToSql不再限制sql的长度</li>
<li>[NEW]方法名生成sql支持mybatis flex框架</li>
</ul>
<ul>
<li>[IMPROVE]check resultMap columns support more complex resultmap</li>
<li>[FIX]fix completion on #{} when disable kotlin plugin</li>
<li>[IMPROVE]support preview xml on intellij community version</li>
<li>[IMPROVE]convert log to sql wont limit sql length</li>
</ul>
<strong>3.2.3</strong>
<ul>
<li>[NEW]like语句后面提示likeUserName这种并且直接bind好</li>
<li>[FIX]select * 不再提示把column加到resultMap中</li>
<li>[FIX]部分用户密文失败修复</li>
<li>[FIX]mybatis log linux系统临时文件夹问题</li>
<li>[IMPROVE]修复使用老版本api annotator可能会导致的性能问题</li>
</ul>
<ul>
<li>[NEW]after like statement will auto bind</li>
<li>[FIX]mybatis log linux temp folder issue</li>
<li>[IMPROVE]fix potential performance issue</li>
</ul>
<strong>3.2.2</strong>
<ul>
<li>[NEW]支持#{}中使用数组操作符解析</li>
<li>[IMPROVE]jdbcType会根据java类型来优先提示</li>
<li>[NEW]检测查询的字段但是resultMap或者resultType中没有并且可以一键加过去</li>
<li>[IMPROVE]支持mybatis generator配置xml后缀</li>
<li>[NEW]支持jakarta注解</li>
<li>[IMPROVE]方法名生成sql支持resultMap extends</li>
<li>[New]从方法名生成到mybatisplus的QueryWrapper</li>
<li>[NEW]生成testcase支持生成到mybatisplus</li>
</ul>
<ul>
<li>[NEW]support #{} use array[] operation</li>
<li>[NEW]detect select column not in resultMap or resultType, can add them quickly to resultMap or resultType</li>
<li>[IMPROVE]support mybatis generator configure xml suffix</li>
<li>[NEW]support jakarta annotation</li>
<li>[IMPROVE]method name to sql support resultMap extends</li>
<li>[New]mybatis plus method name to QueryWrapper</li>
<li>[NEW]generate testcase support mybatisplus</li>
</ul>
<strong>3.2.1</strong>
<ul>
<li>[New]一键将cdata语句转换为&amp;gt;&amp;lt;这种方便SQL进行代码提示</li>
<li>[New]xml上右键可以转换sql到xml,将大于号小于号转换为&amp;lt;&amp;gt;这种</li>
<li>[FIX]controller模版import修复</li>
<li>[FIX]部分机器离线激活出错</li>
<li>[IMPROVE]mybatis log点击parameter log到相同的文件</li>
<li>[IMPROVE]resultMap上autoMapProperty会根据java实体类字段的顺序来匹配 </li>
</ul>
<ul>
<li>[New]convert cdata to &amp;gt;&amp;lt; for sql code completion</li>
<li>[New]right click on xml to convert cdata to &amp;lt;&amp;gt;</li>
<li>[FIX]fix controller template import</li>
<li>[IMPROVE]mybatis log click parameter log to same file</li>
<li>[IMPROVE]resultMap autoMapProperty will keep the order of java class field </li>
</ul>
<strong>3.2.0</strong>
<ul>
<li>[New]支持在map或map.entry类型上foreach</li>
<li>[FIX]修复注解script标签解析依赖kotlin插件</li>
<li>[FIX]生成代码结束的时候有可能导致项目卡住</li>
<li>[FIX]exception修复</li>
</ul>
<ul>
<li>[New]support using collection foreach on map or map.entry type</li>
<li>[FIX]fix annotation sql with script depend on kotlin plugin</li>
<li>[FIX]performance issue after generate code</li>
<li>[FIX]exception fix</li>
</ul>
<strong>3.1.9</strong>
<ul>
<li>[New]支持xml调用枚举或者static变量上的方法解析</li>
<li>[NEW]从模版文件生成代码代码提示支持</li>
<li>[NEW]支持kotlin注解sql</li>
<li>[FIX]mybatis xml未被使用的检测默认开启</li>
<li>[FIX]findByXXBetween当if test null and empty勾选时生成问题</li>
<li>[FIX]社区版使用mybatis database 自定义driver路径报错的问题</li>
</ul>
<ul>
<li>[NEW]support xml use static field or enum with method</li>
<li>[NEW]code completion when use template to generate</li>
<li>[NEW]support kotlin annotation sql</li>
<li>[FIX]mybatis xml unused check enable by default</li>
<li>[FIX]findByXXBetween when if test null and empty is selected generate problem</li>
<li>[FIX]community version use mybatis database driver jar error</li>
</ul>
<strong>3.1.8</strong>
<ul>
<li>[FIX]兼容2023.1最新eap版本</li>
<li>[NEW]支持自定义lombok注解</li>
<li>[IMPROVE]if test代码提示优化</li>
<li>[IMPROVE]xml性能优化</li>
<li>[NEW]迁移到模版生成代码</li>
</ul>
<ul>
<li>[FIX]compatability for 2023.1 eap version</li>
<li>[NEW]support customize lombok annotation</li>
<li>[IMPROVE]if test completion improve</li>
<li>[IMPROVE]xml performance improve</li>
</ul>
<strong>3.1.7</strong>
<ul>
<li>[FIX]兼容2023.1 eap版本</li>
<li>[FIX]修复部分用户激活问题</li>
</ul>
<ul>
<li>[FIX]compatability for 2023.1 eap version</li>
</ul>
<strong>3.1.6</strong>
<ul>
<li>[FIX]修复xml添加注释或空格高亮失效</li>
<li>[NEW]xml测试sql添加All if test true和All if test false</li>
<li>[NEW]生成代码支持生成javax注解@NotNull@Size</li>
<li>[NEW]支持oracle批量插入语句生成</li>
<li>[IMPROVE]inspection性能优化</li>
<li>[FIX]修复getBean方法exception</li>
</ul>

<ul>
    <li>[FIX]fix highlight loss when edit xml</li>
    <li>[NEW]test sql add All if test true and All if test false Action</li>
    <li>[NEW]support generate javax @NotNull @Size annotation</li>
    <li>[IMPROVE]code inspection performance</li>
    <li>[FIX]fix getBean method exception</li>
</ul>
<strong>3.1.5</strong>
<ul>
    <li>[NEW]support parse $ statement by xml tag comment</li>
    <li>[FIX]fix spring mapperscan exception throw when use +</li>
    <li>[NEW]add button to expand * and ** packages to package list</li>
    <li>[IMPROVE]support completion for static field in super class</li>
    <li>[FIX]exception when use intention preview</li>
    <li>[IMPROVE]community version can set driver class and driver path</li>
</ul>

<ul>
    <li>1.支持通过xml标签上的注释来解析$表达式</li>
    <li>2.修复当mapperScan使用+号的报错</li>
    <li>3.提供按钮可以一键把*和**的typeAlias转换为具体包名</li>
    <li>4.支持自动提示父类中的static final字段</li>
    <li>5.修复开启intention preview的代码报错</li>
    <li>6.idea社区版生成代码数据库支持配置驱动</li>
</ul>
<strong>3.1.3</strong>
<ul>
<li>[NEW]support java annotation script tag</li>
<li>[NEW]sql log jump to xml</li>
<Li>[FIX]method name use insertList and insertSelective when resultmap not complete exception</Li>
<li>[NEW]support kotlin mapper scan spring injection</li>
<li>[NEW]support resulthandler type check</li>
<li>[IMPROVE]better completion for ognl and #{}</li>
</ul>
<ul>
<li>1.支持java注解中使用script的识别</li>
<li>2.可以从日志跳转到xml</li>
<li>3.方法名insertList和insertSelective当属性不一致exception修复</li>
<li>4.支持kotlin mapperscan spring注入</li>
<li>5.支持resulthandler类型的检测</li>
<li>6.代码提示优化</li>
</ul>
<strong>3.1.2</strong>
<ul>
<li>[NEW]add option for sql tag auto detect prefix and suffix</li>
<li>[NEW]resultMap add check column menu to check unused column in resultMap related select statement</li>
<Li>[NEW]support icon for base class to xml</Li>
<li>[NEW]support select * in resultMap auto map and check column</li>
<li>[NEW]support to check mybatis interface unused method</li>
</ul>
<ul>
<li>1.添加菜单可以自动识别sql标签的前后缀</li>
<li>2.resultMap添加check column菜单来识别当前resultMap对应的select语句里面未使用的列</li>
<li>3.从基类跳转到xml图标支持</li>
<li>4.resultMap auto map和check column支持识别 select * </li>
<li>5.支持检测mybatis接口中未使用的方法</li>
</ul>
<strong>3.1.1</strong>
<ul>
<li>[FIX]fix when generate test case line seprator issue</li>
</ul>
<ul>
<li>1.修复生成testcase时生成换行符exception</li>
</ul>
<strong>3.1.0</strong>
<ul>
<li>[FIX]when open intention preview, create select statement multiple times</li>
</ul>
<ul>
<li>1.修复开启intention preview, create select statement重复创建的问题</li>
</ul>
<strong>3.0.9</strong>
<ul>
<li>[NEW]mybatis generator save configuration</li>
<li>[NEW]mybatis generator configuration export to json and import from json</li>
<li>[NEW]support xml include with bind names</li>
<li>[NEW]mybatis generator will read line separator from intellij</li>
<li>[FIX]some formatter issue</li>
<li>[FIX]make string null and empty when reference to field and parameter</li>
<li>[IMPROVE] $ replace sql support more pattern</li>
</ul>
<ul>
<li>1.mybatis generator支持保存配置，导入导出配置</li>
<li>2.支持xml include带bind变量的解析</li>
<li>3.一键string判断null和空支持当值来自于字段或者方法参数</li>
<li>4.bug修复
</ul>
<strong>3.0.8</strong>
<ul>
<li>[FIX]string exception when mybatis log has no parameter</li>
<li>[FIX]mybatis log too many memory issue</li>
<li>[NEW]support generate all column sql using template</li>
</ul>
<ul>
<li>1.修复mybatis log当没有参数时的报错</li>
<li>2.修复mybatis log数量太多时内存占用问题</li>
<li>3.表上右键generate all column sql 可以通过模版来生成</li>
</ul>
<strong>3.0.7</strong>
<ul>
<li>[FIX]mybatis interface generate xml when selected interface class name</li>
<li>[IMPROVE]mybatis plus generate updateByPrimaryKeySelective</li>
<li>[IMPROVE]mybatis plus typehandler will add to model class</li>
<li>[IMPROVE]resultMap column auto completion when use with statement</li>
<li>[IMPROVE]support swagger3 openapi annotation</li>
<li>[IMPROVE]support disable param1,param2 like auto completion</li>
<li>[FIX]fix deadLock exception</li>
<li>[FIX]fix mybatis log parameter line contain multiple ending space to sql</li>
</ul>
<ul>
<li>1.修复从接口类生成xml选中类名无法生成</li>
<li>2.优化mybatisplus生成updateByPrimaryKeySelective</li>
<li>3.mybatisplus定制列中配置的typehandler会生成到TableField注解上</li>
<li>4.select使用with语句的resultMap column自动提示的解析</li>
<li>5.表上生成代码支持swagger3，openapi</li>
<li>6.支持配置禁用param1,param2这种代码提示</li>
<li>7.修复deadLock异常</li>
<li>8.修复mybatis log 部分情况无法解析问题</li>
</ul>
<strong>3.0.6</strong>
<ul>
<li>[FIX]sql log parameter contain null value logged sql is null</li>
<li>[IMPROVE]module name can be searched and other ui improvement</li>
<li>[FIX]move annotation to xml when xml not exist generate xml issue</li>
<li>[IMPROVE]create xml for mapper interface</li>
</ul>
<ul>
<li>1.修复sql log 参数值包含null时解析的问题</li>
<li>2.表上生成代码功能module名可以进行搜索和一些其他ui优化</li>
<li>3.修复从注解挪动sql到xml时，xml不存在创建xml</li>
<li>4.优化从接口从生成xml触发问题</li>
</ul>
<strong>3.0.5</strong>
<ul>
<li>[FIX]fix editor null pointer exception</li>
</ul>
<ul>
<li>1.修复editor为null的exception</li>
</ul>
<strong>3.0.4</strong>
<ul>
<li>[FIX]sql log remove duplicate not work in some case</li>
<li>[FIX]sql log support more pattern</li>
<li>[FIX]sql log support multi insert ect</li>
<li>[IMPROVE]better ui</li>
</ul>
<ul>
<li>1.修复sql log移除重复的sql某些情况不生效的问题</li>
<li>2.sql log兼容各种sql</li>
<li>3.sql log支持批量模式，一个parepare 多个parameter那种模式</li>
<li>4.更好的ui</li>
</ul>
<strong>3.0.3</strong>
<ul>
<li>[NEW]支持resultmap中使用constructor，提供自动提示，检测等</li>
<li>[IMPROVE]controller的模版可以自动提示</li>
<li>[IMPROVE]更好的性能</li>
<li>[NEW]mybatis日志转sql支持</li>
<li>[IMPROVE]支持清除表缓存</li>
<li>[FIX]修复idea社区版表生成代码出错 当表含有数据库关键字时</li>
</ul>
<strong>3.0.2</strong>
<ul>
<li>[NEW]支持mybatis注解使用常量的解析</li>
<li>[NEW]支持mybatis注解 #{} 自动提示，检测，重构等</li>
<li>[FIX]修复intention preview 会自动弹出窗口比如使用 generate testcase时</li>
<li>[NEW]支持mybatisplus的分页</li>
<li>[FIX]修复sql标签if test的格式化</li>
<li>[FIX]支持解析接口参数为* extend 这种泛型</li>
<li>[FIX]修复typeMapper配置不生效</li>
</ul>
<strong>3.0.1</strong>
<ul>
<li>[FIX]修复mybatis generator出现null pointer</li>
</ul>
<strong>3.0.0</strong>
<ul>
<li>[FIX]where和trim等标签在换行光标跳转问题修复</li>
<li>[NEW]增加typemapper，可以配置java类型和表字段类型的转换关系</li>
<li>[FIX]修复在xml上右键generate all column转义问题</li>
<li>[FIX]给复杂类型加一个param注解支持解析父类中的属性</li>
<li>[NEW]controller模版添加表注释变量</li>
</ul>
<strong>2.9.9</strong>
<ul>
<li>[FIX]修复xml格式化换行的问题</li>
<li>[NEW]可配置if test格式化不换行</li>
<li>[IMPROVE]定制列里面更好的java类型编辑器</li>
<li>[IMPROVE]生成controller配置src folder和package名可以自动提示</li>
</ul>
<strong>2.9.8</strong>
<ul>
<li>[NEW]添加配置param中忽略解析的类型</li>
<li>[NEW]支持ognl数组操作</li>
<li>[FIX]修复从sql导出java类和resultMap sqlServer出现的exception</li>
<li>[FIX]修复从sql导出java类和resultMap文件没有刷新</li>
<li>[NEW]支持mybatis generator只生成java类</li>
</ul>

<strong>2.9.7</strong>
<ul>
<li>[NEW]支持kotlin添加param注解</li>
<li>[NEW]kotlin接口方法找不到xml中的sql的检测</li>
<li>[FIX]修复mybatis genrator文件夹配置为空的提示的位置</li>
<li>[FIX]修复使用mybatis generator后idea的文件没有刷新出来</li>
</ul>
<strong>2.9.6</strong>
        <ul>
            <li>[FIX]方法名生成sql的exception修复</li>
        </ul>
        <strong>2.9.5</strong>
        <ul>
            <li>[FIX]生成java类时的exception</li>
            <li>[IMPROVE]方法名生成sql可以在reslutMap缺少字段的情况下生成</li>
            <li>[FIX]resultMap的格式化问题</li>
        </ul>
        <strong>2.9.4</strong>
        <ul>
            <li>[FIX]长sql xml文件格式化</li>
            <li>[NEW]支持对复杂类型重构</li>
            <li>[NEW]支持sqlSession 多个xml的跳转</li>
            <li>[FIX]修复swagger注释</li>
        </ul>
        <strong>2.9.3</strong>
        <ul>
            <li>[FIX]修复sql标签带cdata的解析</li>
            <li>[IMPROVE]支持sqlSession调用跳转到xml
            <li>[IMPROVE]支持apple m1芯片
            <li>[FIX]修复$ 的格式化问题
        </ul>
        <strong>2.9.0</strong>
        <ul>
            <li>[IMPROVE]support 2021.1</li>
            <li>[IMPROVE]could config method name generate sql comment style</li>
            <li>[NEW]mybatis generator could preview xml</li>
            <li>[IMPROVE]support mybatisplus table exist false</li>
            <li>[IMPROVE]method name generate sql support if test select all</li>
            <li>[FIX]possible null pointer</li>
        </ul>
        <strong>2.8.9</strong>
        <ul>
            <li>[FIX]intellij community version xml code formatter ognl fix</li>
            <li>[IMPROVE]support 2020.4 version</li>
            <li>[IMPROVE]resultMap column duplicate inspection</li>
            <li>[IMPROVE]better chinese inspection description</li>
            <li>[IMPROVE]support search scope with module and project</li>
            <li>[NEW]could config mybatis sql tag ignore sql syntax error</li>
        </ul>
        <strong>2.8.8</strong>
        <ul>
            <li>[FIX]intellij community version use database generate crud and generate testcase exception</li>
            <li>[IMPROVE]intellij community version no primary key warning</li>
            <li>[IMPROVE]method name generate sql @Transient maven location</li>
            <li>[IMPROVE]resultMap column inspection ignore case</li>
        </ul>
        <strong>2.8.7</strong>
        <ul>
        <li>[FIX]support chinese or japanese in #{}</li>
        <li>[FIX]generate insertOnDuplicateKeySelective string empty check</li>
        <li>[IMPROVE]base support for include with property</li>
        <li>[IMPROVE]generate from database table warning where table dont have primary key</li>
        <li>[NEW]support for 2020.3</li>
        </ul>
        <strong>2.8.6</strong>
        <ul>
        <li>[FIX]fix sql keyword completion after #{}</li>
        <li>[FIX]fix reformat code missing with comment inside sql</li>
        </ul>
        <strong>2.8.4</strong>
        <ul>
        <li>[NEW]fix java inspection performance issue</li>
        </ul>
        <strong>2.8.3</strong>
        <ul>
        <li>[NEW]kotlin method name generate sql</li>
        <li>[IMPROVE]plugin conflict notification</li>
        <li>[IMPROVE]sql dialect not configured notification</li>
        <li>[NEW]could configure to remove some type parameter in mybatis method</li>
        <li>[NEW]could configure eacape all column</li>
        <li>[NEW]generate testcase could configure plugin part</li>
        <li>[NEW]multiple table generate can use actual column name</li>
        </ul>
        <strong>2.8.2.fix-2</strong>
        <ul>
        <li>[FIX]compatible for 2020.2 eap version</li>
        </ul>
        <strong>2.8.2.fix</strong>
        <ul>
        <li>[FIX]fix line indent  create new statement from java method and when type enter</li>
        </ul>
        <strong>2.8.2</strong>
        <ul>
        <li>[NEW]better performance</li>
        <li>[NEW]mybatis sql formatter</li>
        <li>[NEW]resultMap column go to reference, rename</li>
        <li>[FIX]fix using lombok plugin rename resultMap property name start with set</li>
        <li>[FIX]fix mybatis generator with lombok builder annotation</li>
        <li>[FIX]activation and unbind using socks proxy error</li>
        </ul>
        <strong>2.8.1</strong>
        <ul>
        <li>[FIX]generate testcase component exception</li>
        </ul>
        <strong>2.8.0</strong>
        <ul>
        <li>[FIX]fix possible null pointer exception when use project setting page</li>
        <li>[NEW]support mybatis generator with configure method name generate</li>
        <li>[NEW]support 2020 version</li>
        <li>[NEW]better ognl complete and evaluate for bind and collection with method invoke</li>
        <li>[NEW]support kotlin param completion and inspection</li>
        <li>[NEW]add @ignore quick fix in mybatis choose when statement</li>
        <li>[NEW]escape table name when they are keywords</li>
        <li>[IMPROVE]better method name completion</li>
        </ul>
        <strong>2.7.8</strong>
        <ul>
        <li>[FIX]fix swagger exception when column comment is null</li>
        <li>[NEW]support mysql json type</li>
        <li>[NEW]generate all column sql right click on xml</li>
        </ul>
        <strong>2.7.7</strong>
        <ul>
            <li>[NEW]database generate could config method name to generate</li>
            <li>[NEW]support findByAllExceptXXBetween statement</li>
            <li>[NEW]move sql from annotation to xml</li>
            <li>[FIX]test sql will add quote when param is string type</li>
            <li>[NEW]test sql could write and test in the same time</li>
            <li>[NEW]ognl support reference mybatis properties</li>
            <li>[NEW]lombok when has extend add @EqualsAndHashCode(callSuper = true)</li>
            <li>[NEW]support updateBatchSelective</li>
            <li>[NEW]support simple sql reformat</li>
        </ul>
        <strong>2.7.6</strong>
        <ul>
            <li>[NEW]typeAlias support for Intellij community and mybatisPlus</li>
            <li>[NEW]support param using static constant</li>
            <li>[NEW]extract include refid from sql</li>
            <li>[NEW]table name to entity support remove table prefix</li>
            <li>[NEW]generate join support multiple table</li>
            <li>[NEW]database generate crud support oracle sequence</li>
            <li>[NEW]method name generate sql use where tag instead of where 1=1</li>
            <li>[NEW]support 32 system</li>
        </ul>
        <strong>2.7.5</strong>
        <ul>
            <li>[NEW]method name generate sql will not depend on insert method</li>
            <li>[FIX]press enter after if test ect error indent</li>
            <li>[FIX]press enter or delete in blank part cause highlight disappear</li>
            <li>[NEW]ognl support inner class</li>
            <li>[FIX]sql parse error when no blank before param</li>
            <li>[FIX]complete and inspection for param using generic</li>
            <li>[NEW]support 2019.3 version</li>
        </ul>
        <strong>2.7.4</strong>
        <ul>
            <li>[FIX]possible substring exception when edit sql</li>
            <li>[NEW]quick fix for param and ognl</li>
            <li>[NEW]super class invoke could jump to xml</li>
            <li>[FIX]resultMap column auto complete support more sql pattern</li>
            <li>[NEW]generate java method from xml</li>
            <li>[NEW]generate @sql comment for mybatis sql tag</li>
            <li>[NEW]java method return type inspection support @MapKey</li>
            <li>[FIX]if xml select steatment is referenced by resultMap will not show error</li>
            <li>[FIX]database generate crud entity class will remove field in super class</li>
            <li>[FIX]quick fix for resultMap property</li>
            <li>[FIX]param auto completion for unpaid user</li>
        </ul>
        <strong>2.7.3</strong>
        <ul>
            <li>[NEW]resultmap column inspection support columnPrefix</li>
            <li>[FIX]mapper interface with super class generic</li>
            <li>[NEW]use java method to config columnName to propertyName</li>
            <li>[NEW]resultMap jdbcType and typeHandler better auto complete and inspection</li>
            <li>[NEW]generate properties on resultMap will auto match column in select tag</li>
        </ul>
        <strong>2.7.2</strong>
        <ul>
            <li>[NEW]param and ognl refactor</li>
            <li>[NEW]intellij community version param complete</li>
            <li>[IMPROVE]better param completion and inspection for typeHandler and mode and resultMap ect</li>
            <li>[FIX]resultType resultMap inspection</li>
            <li>[NEW]resultMap column inspection</li>
            <li>[FIX]resultMap discriminator support</li>
            <li>[NEW]database generate crud support mybatisPlus2</li>
            <li>[NEW]better merge ui</li>
            <li>[FIX]sql extract resultmap support more sql pattern</li>
            <li>[NEW]kotlin class jump to xml each other</li>
            <li>[FIX]better generic in mapper interface support</li>
            <li>[NEW]support ognl use instanceOf</li>
        </ul>
<strong>2.7.1</strong>
    <ul>
        <li>[NEW]ognl better completion and inspection for single param no annotation</li>
        <li>[FIX]intellij community version typed error</li>
        <li>[FIX]support 2019.2 version</li>
        <li>[NEW]add checkBlobColumn option </li>
        <li>[FIX]check conflict for exampleQuery and tkMapper</li>
        <li>[NEW]comment in sql use xml comment instead of sql</li>
    </ul>

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
