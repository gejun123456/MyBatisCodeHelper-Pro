<strong>3.4.5</strong>
<ul>
<li>[NEW]mybatis generator通过已经存在的xml文件快速配置好包名</li>
<li>[NEW]支持select provider跳转到mapper方法</li>
<li>[FIX]修复部分项目生成join时关联xml文件没有代码提示</li>
<li>[IMPROVE]mybatisplus项目可以选择不生成tableField注解</li>
<li>[IMPROVE]日志转sql可以配置忽略比如一些日志表</li>
</ul>
<ul>
<li>[NEW]Mybatis generator quick set packages by existing xml file</li>
<li>[NEW]Support select provider jump to mapper method</li>
<li>[IMPROVE]Mybatisplus not generate tableField annotation</li>
<li>[FIX]Fix xml file code completion not work when generate join</li>
<li>[IMPROVE]Log to sql could config to ignore some log tables</li>
</ul>
<strong>3.4.3</strong>
<ul>
<li>[IMPROVE]修复mapper直接调用的方法名提示重复的问题</li>
<li>[IMPROVE]支持自定义注解any类型以及添加注释</li>
<li>[FIX]修复$表达式添加注释问题</li>
</ul>
<ul>
<li>[IMPROVE]Fix duplicate method name prompt for mapper direct call</li>
<li>[IMPROVE]Support custom annotation any type and add column remarks</li>
<li>[FIX]Fix $ expression add replace comment issue</li>
</ul>
<strong>3.4.2</strong>
<ul>
<li>[IMPROVE]支持字段自定义注解比如Jackson</li>
<li>[IMPROVE]mybatis log转sql性能优化</li>
<li>[IMPROVE]生成testcase自动检测junit平台</li>
</ul>
<ul>
<li>[IMPROVE]Support custom annotations like jackson</li>
<li>[IMPROVE]Performance optimization for mybatis log to sql conversion</li>
<li>[IMPROVE]Auto-detect junit platform when generating testcase</li>
</ul>
<strong>3.4.1</strong>
<ul>
<li>[FIX]修复报错PsiInvalidElementAccessException</li>
</ul>
<ul>
<li>[FIX]Fix Exception PsiInvalidElementAccessException</li>

</ul>
<strong>3.4.0</strong>
<ul>
<li>[IMPROVE]直接在mapper. 调用时就进行方法名提示和生成代码</li>
<li>[IMPROVE]生成openApi等注解时兼容注释换行</li>
<li>[IMPROVE]参数是map类型时不再进行标红</li>
<li>[IMPROVE]在sql标签上面添加$sql注释不生效的问题</li>
</ul>
<ul>
<li>[IMPROVE] Direct code suggestions and generation when typing from mapper. call.</li>
<li>[IMPROVE] Compatible with comment line breaks when generating OpenAPI and other annotations.</li>
<li>[IMPROVE] No longer highlights errors when the parameter is of Map type.</li>
<li>[IMPROVE] Fixed the issue where $sql comments did not take effect above the sql tag.</li>
</ul>
<strong>3.3.9</strong>
<ul>
<li>[IMPROVE]生成resultMap时id放在第一位</li>
<li>[FIX]修复未激活用户使用部分功能报错</li>
<li>[IMPROVE]激活代理优化</li>
</ul>
<ul>
<li>[IMPROVE] Place `id` first when generating `resultMap`</li>
</ul>
<strong>3.3.8</strong>
<ul>
<li>[NEW]kotlin方法名生成sql优化</li>
<li>[NEW]生成batchInsertOnDuplicate方法</li>
<li>[NEW]优化mybatisplus和更多sql insertOrUpdate方法名冲突问题</li>
<li>[NEW]点击parameter跳转到最终sql支持配置最大字符避免控制台卡顿</li>
<li>[NEW]model class支持配置前缀</li>
<li>[IMPROVE]格式化优化</li>
</ul>
<ul>
<li>[NEW] Optimize Kotlin method name generation for SQL</li>
<li>[NEW] Add support for generating `batchInsertOnDuplicate` method</li>
<li>[NEW] Resolve method name conflicts for `insertOrUpdate` in MyBatis-Plus and other SQL scenarios</li>
<li>[NEW] Support configuring maximum characters for jumping to final SQL from parameters to prevent console lag</li>
<li>[NEW] Add prefix configuration support for model classes</li>
<li>[IMPROVE] Formatting optimization</li>
</ul>
<strong>3.3.7</strong>
<ul>
<li>[NEW]支持多层sql标签代码提示和检测</li>
<li>[NEW]支持全局替换$表达式解析</li>
<li>[IMPROVE]更好的clickhouse支持</li>
<li>[FIX]xml使用enter可能不换行的问题</li>
<li>[IMPROVE]更好的2024.3支持</li>
<li>[NEW]兼容kotlin k2 mode</li>
</ul>
<ul>
<li>[NEW] Support for multi-layer SQL tag code completion and inspection</li>
<li>[NEW] Support for global replacement of $ expression parsing</li>
<li>[IMPROVE] Enhanced support for ClickHouse</li>
<li>[FIX] Issue where pressing Enter in XML might not create a new line</li>
<li>[IMPROVE]better support for 2024.3</li>
<li>[NEW]support kotlin k2 mode</li>
</ul>
<strong>3.3.6</strong>
<ul>
<li>[NEW]兼容2024.3</li>
<li>[IMPROVE]提示优化</li>
<li>[FIX]mybatisplus支持生成updateByPrimaryKey</li>
<li>[FIX]updateBatch方法名冲突</li>
</ul>
<ul>
<li>[NEW] Compatibility with 2024.3</li>
<li>[IMPROVE] Prompt optimization</li>
<li>[FIX] MyBatisPlus support for generating updateByPrimaryKey</li>
<li>[FIX] Name conflict for updateBatch method</li>
</ul>
<strong>3.3.5</strong>
<ul>
<li>[FIX]sql标签${}来自include property时代码提示和检测</li>
<li>[FIX]2024.1版本后插件的中文失效问题修复</li>
</ul>
<ul>
<li>[FIX]support ${} from include property completion and inspection</li>
<li>[FIX]could configure language for plugin</li>
</ul>
<strong>3.3.4</strong>
<ul>
<li>[FIX]2024.1.4写typeHandler时不会补全包名的问题</li>
<li>[IMPROVE]把查询的字段加入到resultMap或resultType时会去根据数据库字段的类型给出字段的java类型</li>
<li>[NEW]sql log转sql时格式化优化</li>
<li>[FIX]resultMap支持多层的columnPrefix解析</li>
<li>[IMPROVE]生成代码支持配置xml文件和mapper文件的前缀</li>
<li>[IMPROVE]调整测试sql时输入框的大小</li>
</ul>
<ul>
<li>[FIX]2024.1.4 package is not auto completed when write typeHandler ect</li>
<li>[IMPROVE]When add unused selected column to resultMap or resultType will detect column java type by database columns</li>
<li>[NEW]Better formatter for mybatis log to sql</li>
<li>[FIX]Support multiple columnPrefix when add column to resultMap inspection</li>
<li>[IMPROVE]Generate code support xml prefix and mapper prefix</li>
<li>[IMPROVE]Run sql better text field size</li>
</ul>
<strong>3.3.3</strong>
<ul>
<li>[FIX]2024.1.2生成testcase没反应的问题</li>
<li>[IMPROVE]service interface可以自定义类名</li>
<li>[NEW]支持注解sql测试</li>
<li>[FIX]exception修复</li>
</ul>
<ul>
<li>[FIX]2024.1.2 Generate testcase not work</li>
<li>[IMPROVE]Service interface can customize class name</li>
<li>[NEW]Support run sql for mybatis annotation</li>
<li>[FIX]exception fix</li>
</ul>
<strong>3.3.2</strong>
<ul>
<li>[FIX]idea社区版无法链接数据库的问题</li>
<li>[IMPROVE]xml运行sql 支持通过参数来给if test设置值</li>
<li>[FIX]exception修复</li>
</ul>
<ul>
<li>[FIX] Issue with IDEA Community Edition unable to connect to databases</li>
<li>[IMPROVE] XML SQL execution now supports setting values for 'if test' conditions via parameters</li>
<li>[FIX]exception fix</li>
</ul>
<strong>3.3.1</strong>
<ul>
<li>[FIX]2024.1 xml上无法运行sql的问题</li>
<li>[IMPROVE]支持select语句以include开头时resultMap column代码提示和检测</li>
<li>[IMPROVE]添加选项支持以parameterType作为参数类型解析当接口参数为父类时</li>
</ul>
<ul>
<li>[FIX]2024 xml execute sql issue</li>
<li>[IMPROVE]support resultMap column completion and inspection when select is start with include</li>
<li>[IMPROVE]add option to use parameter type to resolve when method parameter type is super class</li>
</ul>
<strong>3.3.0</strong>
<ul>
<li>[IMPROVE]兼容2024.1版本</li>
<li>[IMPROVE]检测select字段resultType中不存在时可以批量加入到类中</li>
<li>[IMPROVE]mybatisplus自动检测主键是否应该设置为Auto</li>
<li>[FIX]mybatis ognl单数参数可以任意名字引用当类型是Collection类型的支持</li>
</ul>
<ul>
<li>[IMPROVE]compatability for 2024.1 version</li>
<li>[IMPROVE]inspection on select column add to resultType</li>
<li>[IMPROVE]mybatisplus auto detect IdType Auto</li>
<li>[FIX]mybatis ognl单数参数可以任意名字引用当类型是Collection类型的支持</li>
</ul>
<strong>3.2.9</strong>
<ul>
<li>[IMPROVE]kotlin报错优化</li>
<li>[IMPROVE]支持mybatis ognl单个参数可以使用任意名字引用</li>
<li>[IMPROVE]提供界面来合并xml代码</li>
<li>[FIX]support ognl use any name for single parameter when type is from Collection</li>
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
<li>[IMPROVE]postgresql keyword use double quote</li>
<li>[IMPROVE]module name can be searched and other ui improvement</li>
<li>[FIX]move annotation to xml when xml not exist generate xml issue</li>
<li>[IMPROVE]create xml for mapper interface</li>
</ul>
<ul>
<li>1.修复sql log 参数值包含null时解析的问题</li>
<li>2.表上生成代码功能module名可以进行搜索和一些其他ui优化</li>
<li>3.修复从注解挪动sql到xml时，xml不存在创建xml</li>
<li>4.优化从接口从生成xml触发问题</li>
<li>5.postgresql使用关键字时使用双引号来转义</li>
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
<li>[NEW]support result map use constructor</li>
<li>[IMPROVE]better controller template provide auto completion</li>
<li>[IMPROVE]better error reporter</li>
<li>[IMPROVE]better performance</li>
<li>[NEW]mybatis sql log to real sql support</li>
<li>[IMPROVE]support clear table config for mybatis generator</li>
<li>[FIX]intelllij community generate code when table use key word</li>
</ul>
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
<li>[NEW]mybatis annotation constant support</li>
<li>[NEW]mybatis annotation param auto completion,inspection,rename ect</li>
<li>[NEW]mybatis annotation sql injection</li>
<li>[FIX]intention action preview will not show dialog when use genreate testcase ect</li>
<li>[NEW]support page query for mybatisplus</li>
<li>[FIX]sql formatter for mybatis sql tag with if test</li>
<li>[FIX]support type * extends</li>
<li>[FIX]type mapper not work</li>
</ul>
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
<li>[FIX]mybatis generator set text null pointer</li>
</ul>
<ul>
<li>[FIX]修复mybatis generator出现null pointer</li>
</ul>
<strong>3.0.0</strong>
<ul>
<li>[FIX]mybatis where or trim tag focus change after completion</li>
<li>[NEW]add typeMapper for column type and java type mapping</li>
<li>[FIX]right click on xml generate all column sql when column using database keyword escape issue</li>
<li>[FIX]refactor add param for complex type when type has base class refactor them as well</li>
<li>[NEW]update controller template with tableRemark variable</li>
</ul>
<ul>
<li>[FIX]where和trim等标签在换行光标跳转问题修复</li>
<li>[NEW]增加typemapper，可以配置java类型和表字段类型的转换关系</li>
<li>[FIX]修复在xml上右键generate all column转义问题</li>
<li>[FIX]给复杂类型加一个param注解支持解析父类中的属性</li>
<li>[NEW]controller模版添加表注释变量</li>
</ul>
<strong>2.9.9</strong>
<ul>
<li>[FIX]xml sql code formatter line issue</li>
<li>[NEW]add configuration for if test not split line</li>
<li>[IMPROVE]better java type editor for customized column</li>
<li>[IMPROVE]controller package and src folder auto completion</li>
</ul>
<ul>
<li>[FIX]修复xml格式化换行的问题</li>
<li>[NEW]可配置if test格式化不换行</li>
<li>[IMPROVE]定制列里面更好的java类型编辑器</li>
<li>[IMPROVE]生成controller配置src folder和package名可以自动提示</li>
</ul>
<strong>2.9.8</strong>
<ul>
<li>[NEW]add support for skip analyze param type</li>
<li>[NEW]support ognl array operation</li>
<li>[FIX]fix sql generate java class and resutlMap exception when use sqlserver</li>
<li>[FIX]fix sql generate java class file not refereshed after generated </li>
<li>[NEW]support only generate model in mybatis generator</li>
</ul>
<ul>
<li>[NEW]添加配置param中忽略解析的类型</li>
<li>[NEW]支持ognl数组操作</li>
<li>[FIX]修复从sql导出java类和resultMap sqlServer出现的exception</li>
<li>[FIX]修复从sql导出java类和resultMap文件没有刷新</li>
<li>[NEW]支持mybatis generator只生成java类</li>
</ul>
<strong>2.9.7</strong>
<ul>
<li>[NEW]support kotlin add param</li>
<li>[NEW]kotlin method not found in xml inspection</li>
<li>[FIX]fix error notify location when use mybatis generator</li>
<li>[FIX]fix file not refresh in idea when use mybatis generator </li>
</ul>
<ul>
<li>[NEW]支持kotlin添加param注解</li>
<li>[NEW]kotlin接口方法找不到xml中的sql的检测</li>
<li>[FIX]修复mybatis genrator文件夹配置为空的提示的位置</li>
<li>[FIX]修复使用mybatis generator后idea的文件没有刷新出来</li>
</ul>

<strong>2.9.6</strong>
<ul>
<li>[FIX]method generate xml statement exception</li>
</ul>
<strong>2.9.5</strong>
<ul>
<li>[FIX]generate java class use swagger exception</li>
<li>[IMPROVE]method name generate sql could ignore lacked fields</li>
<li>[FIX]resultMap id and result with end tag formatting issue</li>
</ul>
<strong>2.9.4</strong>
<ul>
<li>[FIX]sql formatter not work with long sql</li>
<li>[NEW]support refactor add a param name to a complex type</li>
<li>[NEW]support sql session select multiple xml jump</li>
<li>[FIX]fix swagger class comment</li>
</ul>
<strong>2.9.3</strong>
<ul>
<li>[FIX]fix sql tag with cadata parsing</li>
<li>[IMPROVE]support sqlSession select statement jump to xml
<li>[IMPROVE]support apple m1
<li>[FIX]fix formatter with $ with cdata issue
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
<strong>2.7</strong>
<ul>
<li>[NEW]ognl support for if test when test foreach collection </li>
<li>[FIX]java utils null pointer exception when setter method not return void</li>
<li>[IMPROVE]param auto complete in cdata block</li>
<li>[FIX]example query generated service List is not import</li>
<li>[FIX]java.lang.RunTimeException:After patch:doc</li>
<li>[FIX]database generate crud press enter will not exit</li>
<li>[FIX]if test string compare with single char inspection</li>
<li>[FIX]type safe mybatis sql with @ignoreSql @sql $sql comments</li>
<li>[NEW]method return type inspection</li>
<li>[NEW]database regenerated java class could merge by ui</li>
<li>[FIX]p3c comment id problem</li>
<li>[IMPROVE]other fix</li>
</ul>
<strong>2.6.1</strong>
<ul>
<li>[FIX]completion kotlin null pointer exception</li>
<li>[IMPROVE]better method name auto complete</li>
<li>[FIX]fix caret point to method body when generate select statement from method</li>
</ul>
<strong>2.6</strong>
<ul>
<li>[NEW]mybatis param inspection</li>
<li>[IMPROVE]better param auto complete</li>
<li>[IMPROVE]better method name auto complete for method name to sql</li>
<li>[IMPROVE]resultMap property auto complete and rename support set method and field</li>
<li>[NEW]support bind tag in xml</li>
<li>[NEW]mapperScan package auto compelte and inspection</li>
<li>[IMPROVE]reformat code after add param action</li>
<li>[FIX]oracle findFirst generate sql not right</li>
<li>[FIX]generate testcase in maven project exception</li>
<li>NEW]support mybatis useActualParamName</li>
<li>[FIX]service not import list when database generate crud</li>
<li>[FIX]database generate crud resource folder not provide package from resource</li>
<li>[FIX]database generate crud mapperAnnotation not remembered</li>
<li>[NEW]database to crud support mybatis plus generate service</li>
<li>[NEW]generate join query support tk mapper and mybatisplus</li>
<li>[FIX]possible exception fix</li>
</ul>
<strong>2.5</strong>
<ul>
<li>[NEW]generate join statement from xml</li>
<li>[IMPROVE]shorten xml comment</li>
<li>[IMPROVE]mark blob column as common column</li>
<li>[IMPROVE]database generate crud could generate service interface</li>
<li>[NEW]support updateByXXX statement</li>
<li>[NEW]better support for sqlServer</li>
<li>[NEW]could customize database generate curd methods</li>
<li>[IMPROVE]better ui for database generate crud</li>
<li>[FIX]null pointer exception ModuleRootManager</li>
<li>[FIX]hashMap$Node cast exception</li>
<li>[NEW]could config auto fold xml generated methods</li>
<li>[NEW]auto complete for mybatis selectKey</li>
</ul>
<strong>2.4</strong>
<ul>
<li>[IMPROVE]generate java class support lombok Serializable ect</li>
<li>[IMPROVE]generate testcase will auto config typeAlias</li>
<li>[IMPROVE]support findAllByXXX ect</li>
<li>[IMPROVE]database generate crud choose not generate jdbcType</li>
<li>[IMPROVE]mybatis configuration file mapper resource auto complete</li>
<li>[FIX]java to select provider will use current module and dependency</li>
<li>[IMPROVE]better performance for typeAlias support</li>
<li>[FIX]mybatis datasource use java8 localDate ect not function</li>
<li>[NEW]database could generate batchInsert,batchUpdate ect</li>
<li>[IMPROVE]add file header when database generate curd like @author</li>
<li>[IMPROVE]findByXXIn will use Collection as param instead of List</li>
<li>[IMPROVE]database regenerate model will ignore transient field and it's getter and setter</li>
</ul>
<strong>2.3</strong>
<ul>
<li>[IMPROVE]springboot typealias support</li>
<li>[IMPROVE]xml inspection on resultMap resultType parameterType ect</li>
<li>[IMPROVE]sql param auto complete in multiple foreach tag</li>
<li>[IMPROVE]regenerate service will merge content</li>
<li>[IMPROVE]update delete count could use if test when using method name generate sql</li>
<li>[IMPROVE]findByAll generate use domain entity as param</li>
<li>[IMPROVE]generate testcase could use database from intellij and history</li>
<li>[FIX]fix exception when using typealias</li>
<li>[NEW]database generate crud could add batchInsert, batchUpdate, InsertOnDuplicate methods</li>
<li>[IMPROVE]support multiple xml with same namespace when using methodName generate sql</li>
<li>[FIX]fix oracle param auto complete exception</li>
<li>[IMPROVE]better format when using method name generate sql</li>
</ul>
<strong>2.2</strong>
<ul>
<li>[FIX]fix mybatis generator regenerate toString equal hashCode not overwrite</li>
<li>[FIX]possible exception fix</li>
<li>[IMPROVE]method generate sql will escape sql keywords</li>
<li>[IMPROVE]mybatis generator mapper suffix could configure</li>
</ul>
<strong>2.1</strong>
<ul>
<li>[New]quick execute mybatis sql from sql statement</li>
<li>[IMPROVE]java generate crud could use other module path</li>
<li>[IMPROVE]support collection array no param auto complete</li>
<li>[IMPROVE]auto escape sql keywords for tk mapper and mybatisplus</li>
<li>[IMPROVE]method name generate sql could use select get query alias ect</li>
</ul>
<strong>2.0.3</strong>
<ul>
<li>[FIX]generate test case database url use utc instead of local time zone</li>
<li>[New]use mybatis generator for multiple table generate</li>
<li>[IMPROVE]tk mapper could config is super class</li>
<li>[NEW]use mybatis generator could generate service</li>
<li>[IMPROVE]auto complete for when statement and resultMap jdbcType</li>
<li>[IMPROVE]resultMap and refId provide complete from other mybatis file</li>
<li>[FIX]oracle using with tk mapper column annotation using ' not recognized</li>
<li>[NEW]mybatis sql tag auto complete for columns</li>
<li>[NEW]resultMap column auto complete based on property name</li>
<li>[NEW]could add schema name to table name</li>
</ul>
<strong>2.0.2</strong>
<ul>
<li>[FIX]oracle date type with jdbcType date instead of timeStamp</li>
<li>[New]database generate crud support common mapper and mybatisPlus</li>
<li>[FIX]indexNotReady exception when generate testcase</li>
<li>[FIX]mapper definition search threading exception</li>
<li>[FIX]method name generate sql possible exception</li>
<li>[IMPROVE]when database contains too many table, connect to database very snow</li>
<li>[IMPROVE]better ui for setting page</li>
<li>[IMPROVE]mybatis spring support * and ** wildcard</li>
<li>[New]method name generate sql support common mapper and mybatisPlus new and old version</li>
<li>[IMPROVE]sql param auto complete with jdbcType</li>
<li>[FIX]postgresql numeric with no length should use bigDecimal instead of short</li>
<li>[IMPROVE]make domain class comment better</li>
<li>[IMPROVE]findByLike will add % to it</li>
<li>[FIX]possible bug when using ctrl+alt+b to jump to xml</li>
</ul>
<strong>2.0.1</strong>
<ul>
<li>[IMPROVE]jump to mapper interface after database generate crud</li>
<li>[NEW]support add swagger annotation when database generate crud</li>
<li>[NEW]could use ctrl+alt+b to jump from mapper method to xml</li>
<li>[New]could jump from resultMap property to java field</li>
<li>[IMPROVE]auto detect table generated key when database generate crud</li>
<li>[IMPROVE]jump to mapper interface after database generate crud</li>
<li>[FIX]exception when use alt+enter generate method xml</li>
<li>[IMPROVE]auto add delimter when database generate crud</li>
<li>[IMPROVE]support mybatis annotation string concat inject sql language</li>
<li>[FIX]possible file not update when generate class already exist</li>
<li>[IMPROVE]java generate crud better ui</li>
<li>[NEW]customize fields when database generate curd javaType could auto complete</li>
</ul>
<strong>2.0.0</strong>
<ul>
<li>recognize mybatis tag in xml, like where trim update ect,provide sql completion after those tag</li>
<li>could generate java class for database table</li>
<li>generate sql column list base on database table</li>
<li>better support for generate page query in mybatis interface method</li>
<li>support findByTrue findByFalse for method name generate sql</li>
<li>if test completion support list check size and string check empty</li>
<li>when use mybatis generator when database, support implement Serializable</li>
</ul>
<strong>1.9.9</strong>
<ul>
<li>fix java generate crud just ignore static fields</li>
<li>auto inject sql language to mybatis annotation sql statement</li>
<li>add mybatis annotation param auto complete</li>
<li>support if test on string check null and empty</li>
<li>generate all properties base on resultMap type collection javaType ect</li>
<li>mybatis annotation sql could auto complete</li>
<li>fix some bug</li>
</ul>
<strong>1.9.8</strong>
<ul>
<li>use database to generate crud support java8 localDateTimeEct</li>
<li>could generate java class and resultMap from xml sql</li>
<li>fix log4j class loader bug</li>
</ul>
<strong>1.9.5</strong>
<ul>
<li>fix bug with spring using @MapperScan not recognized</li>
<li>fix some user might need to reactivate when they change mac address</li>
</ul>
<strong>1.9.4</strong>
<ul>
<li>better support for multiple module project</li>
<li>fix generate test on multiple module project</li>
<li>show user expire date on setting</li>
<li>fix postgresql insert statement serial type should not insert primay key</li>
<li>fix generate test for mybaits annotation</li>
</ul>
<strong>1.9.3</strong>
<ul>
<li> fix method generate sql table name stay the same format</li>
<li> could use method name insertList,insertSelective to generate query</li>
<li> fix possible null pointer</li>
</ul>
<strong>1.9.2</strong>
<ul>
<li> fix using intellij database to generate crud code, mysql dateTime jdbcType is Date instead of TimeStamp</li>
<li> database generate crud package name could auto complete</li>
</ul>
<strong>1.9.1</strong>
<ul>
<li> fix using intellij database to generate crud code, mysql bigInt the default java type is Integer</li>
</ul>
<h4>1.9.0</h4>
<ul>
<li> fix setting not apply after intellij restart</li>
</ul>

<h4>1.8.9</h4>
<ul>
<li>better icon</li>
<li>database generate support lombok, mapperAnnotation</li>
<li>fix bug when using alt+enter on method name</li>
<li>improve generate page statement<li>
<li>support postgresql for java generate crud code<li>
<li>fix checkbox can't select problem</li>
<li>improve generate testcase from mybatis mapper</li>
<li>improve generate page query from mybatis mapper</li>
</ul>

<h4>1.8.8</h4>
<ul>
<li>better indexer</li>
<li>generate page query for mybatis method</li>
</ul>

<h4>1.8.7</h4>
<ul>
<li>add code inspection for xml result map</li>
<li>support more for xml auto complete</li>
<li>could use mybatis on Intellij Ultimate database</li>
<li>bug fix</li>
</ul>

<h4>1.8.6</h4>
<ul>
<li>fix spring integration for 2018.1</li>
<li>fix resultMap property auto complete</li>
<li>fix check result map warning</li>
</ul>

<h4>1.8.5</h4>
<ul>
<li>bug fix</li>
</ul>

<h4>1.8.4</h4>
<ul>
<li>could customize when using database to generate</li>
<li>support param auto complete</li>
<li>better ui from qq group user</li>
<li>add support for spring could recognize mapper mapperScan annotation ect</li>
</ul>

<h4>1.8.3</h4>
<ul>
<li>generate testcase by one click</li>
<li>still show database when can't connect</li>
<li>offline activation support</li>
<li>unbind support</li>
<li>fix no need to focus on table to use mybatis generator</li>
<li>other bug fix</li>
</ul>

<h4>1.8.2</h4>
<ul>
<li>fix mysql using mybatis generator xml using database name</li>
</ul>

<h4>1.8.1</h4>
<ul>
<li>add database support for sqlserver and oracle 10g and mysql8.0</li>
<li>fix BaseColumnList duplicate generate</li>
<li>fix update when xml has comments</li>
<li>using project scope instead of module scope</li>
<li>support annotation like insertProvider ect</li>
</ul>


<h4>1.8.0</h4>
<ul>
<li>support extend on resultMap</li>
<li>add database support oracle and postgresql</li>
<li>better ui for using mybatis generator on database</li>
<li>import param class</li>
<li>fix possible bug</li>
</ul>


<h4>1.7.9</h4>
<ul>
<li>bug fix</li>
</ul>

<h4>1.7.8</h4>
<ul>
<li>fix qq group id</li>
<li>bug fix</li>
</ul>

<ul>
<li>could jump direct from java class to mapper</li>
<li>add param annotation for mybatis mapper</li>
<li>update charset to uft8mb4</li>
<li>fix findByLike problem</li>
</ul>

<h4>1.7.6</h4>
<ul>
<li>mybatis generator using database comment</li>
<li>fix error when generate mybatis generator xml file</li>
<li>fix use project scope when user use mybatis generator</li>
<li>support when one mapper to multiple xml</li>
</ul>

<h4>1.7.5</h4>
<ul>
<li>remember user config path</li>
<li>add keymap to jump from java to xml and xml to java</li>
<li>user could config using project or module search scope</li>
<li>fix encoding problem when using with mybatis generator</li> </ul>

<h4>1.7.4</h4>
<ul>
<li>xml not find in method using warn instead of error</li>
<li>support add jdbcType when update java class field</li>
<li>generate mybatis generator file one click</li>
<li>fix like problem</li>
</ul>

<h4>1.7.3</h4>
<ul>
<li>fix thread assertion bug</li>
<li>mybatis generate not change dao file</li>
 <li>fix java dateTime jdbcType</li>
</ul>

<h4>1.7.2</h4>
<ul>
<li>fix inspection for check mybatis xml not used</li>
</ul>

<h4>1.7.1</h4>
<ul>
<li>support bind on mac address on device register</li>
<li>fix order by with multiple field</li>
<li>fix display probelm on mac when generate files</li>
<li>fix exception on intellij on 1.7.3</li>
<li>add override when generate service impl</li>
<li>add scroll panel for generate by datasource</li>
<li>delete multiple unused xml fast</li>
</ul>

<h4>1.7.0</h4>
<ul>
<li>generate service add override annotation</li>
<li>find first n return list</li>
<li>import java class package when generate service interface</li>
</ul>

<h4>1.6.9</h4>
<ul>
<li>better method name auto complete</li>
<li>fix connect to sql database</li>
<li>fix jdbcType for long</li>
<li>better way to choose package</li>
<li>find one not generate on limit</li>
<li>support using transient</li>
</ul>

<h4>1.6.8</h4>
<ul>
<li>fix icon in xml miss</li>
<li>support more from field comment</li>
<li>support change icon</li>
<li>generate with jdbcType</li>
</ul>

<h4>1.6.7</h4>
<ul>
<li>fix bug service interface import page</li>
<li>could generate comment from field comment</li>
<li>use better icon</li>
<li>support language like updateIncVersion</li>
</ul>

<h4>1.6.6</h4>
<ul>
<li>fix bug when generate method xml in service</li>
</ul>

<h4>1.6.5</h4>
<ul>
<li>support findWithPage</li>
<li>support to configure mapper prefix</li>
</ul>

<h4>1.6.4</h4>
<ul>
<li>support sqlite</li>
<li>oracle support multiple column index,multiple column unique</li>
</ul>

<h4>1.6.0</h4>
<ul>
<li>support generate if test</li>
<li>support generate in service and service interface</li>
<li>support multiple column index,multiple column unique</li>
<li>support generate on function</li>
<li>support generate dto when find more than one field</li>
<li>not using pojo as default param</li>
</ul>
<h4>1.4.5</h4>
<ul>
<li>support with enum type</li>
</ul>
<h4>1.4.4</h4>
<ul>
<li>fix exception when start up</li>
</ul>
<h4>1.4.3</h4>
<ul>
<li> support multiple method xml generate</li>
<li> support for mybatis plus</li>
<li> support domain class with protected field and static field</li>
<li> support for small resolution</li>
<li>bugfix - fix can't generate to path</li>
</ul>
<h4>1.4.2</h4>
<ul>
<li>bugfix - fix Could not initialize class com.ccnode.codegenerator.freemarker.TemplateUtil</li>
</ul>
<h4>1.4.1</h4>
<ul>
<li>bugfix - oralce insertList</li>
<li>bugfix - import issue</li>
</ul>

<h4>1.4</h4>
<ul>
<li>add support for oracle</li>
<li>config use generate key</li>
<li>auto complete for resultMap,refid,keyProperty,property</li>
<li>support with java.sql.Timestamp java.sql.Date java.sql.Time Enum LocalDateTime LocalDate</li>
<li>support update field with insertSelective</li>
<li>add new icon of mybatis jump to xml ect</li>
</ul>

<h4>1.3</h4>
<ul>
<li>add index column and hasDefault column when generate mybatis files</li>
<li>jump from refid resultMap to their definition in mybatis xml. could refactor as well</li>
<li>could refactor method name in xml</li>
<li>add insertSelective when generate mybatis files</li>
<li>generate for greaterThanOrEqualTo and lessThanOrEqualTo and betweenOrEqualTo</li>
<li>add configuration to use with @Mapper</li>
<li>fix not null issue for find module - bug fix</li>
</ul>

<h4>1.2</h4>
<ul>
<li>add support for unsigned type, small int.</li>
<li>check for using object type instead of primitive type</li>
<li>support more auto completion for sql</li>
<li>double type support - bug fix</li>
<li>update field exception -bug fix</li>
</ul>
