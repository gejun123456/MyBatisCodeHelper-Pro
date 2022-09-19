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
<li>[NEW]support result map use constructor</li>
<li>[IMPROVE]better controller template provide auto completion</li>
<li>[IMPROVE]better error reporter</li>
<li>[IMPROVE]better performance</li>
<li>[NEW]mybatis sql log to real sql support</li>
<li>[IMPROVE]support clear table config for mybatis generator</li>
<li>[FIX]intelllij community generate code when table use key word</li>
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
<strong>3.0.1</strong>
<ul>
<li>[FIX]mybatis generator set text null pointer</li>
</ul>
<strong>3.0.0</strong>
<ul>
<li>[FIX]mybatis where or trim tag focus change after completion</li>
<li>[NEW]add typeMapper for column type and java type mapping</li>
<li>[FIX]right click on xml generate all column sql when column using database keyword escape issue</li>
<li>[FIX]refactor add param for complex type when type has base class refactor them as well</li>
<li>[NEW]update controller template with tableRemark variable</li>
</ul>
<strong>2.9.9</strong>
<ul>
<li>[FIX]xml sql code formatter line issue</li>
<li>[NEW]add configuration for if test not split line</li>
<li>[IMPROVE]better java type editor for customized column</li>
<li>[IMPROVE]controller package and src folder auto completion</li>
</ul>
<strong>2.9.8</strong>
<ul>
<li>[NEW]add support for skip analyze param type</li>
<li>[NEW]support ognl array operation</li>
<li>[FIX]fix sql generate java class and resutlMap exception when use sqlserver</li>
<li>[FIX]fix sql generate java class file not refereshed after generated </li>
<li>[NEW]support only generate model in mybatis generator</li>
</ul>
<strong>2.9.7</strong>
<ul>
<li>[NEW]support kotlin add param</li>
<li>[NEW]kotlin method not found in xml inspection</li>
<li>[FIX]fix error notify location when use mybatis generator</li>
<li>[FIX]fix file not refresh in idea when use mybatis generator </li>
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
                <li>[IMPROVE]auto add delemeter when database generate crud</li>
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
    <p><h4>1.9.0</h4>
            <ul>
                <li> fix setting not apply after intellij restart</li>
            </ul>
    </p>
    <p><h4>1.8.9</h4>
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
    </p>
    <p><h4>1.8.8</h4>
            <ul>
                <li>better indexer</li>
                <li>generate page query for mybatis method</li>
            </ul>
    </p>
    <p><h4>1.8.7</h4>
            <ul>
                <li>add code inspection for xml result map</li>
                <li>support more for xml auto complete</li>
                <li>could use mybatis on Intellij Ultimate database</li>
                <li>bug fix</li>
            </ul>
    </p>
    <p><h4>1.8.6</h4>
            <ul>
                <li>fix spring integration for 2018.1</li>
                <li>fix resultMap property auto complete</li>
                <li>fix check result map warning</li>
            </ul>
    </p>
    <p><h4>1.8.5</h4>
            <ul>
                <li>bug fix</li>
            </ul>
    </p>
    <p><h4>1.8.4</h4>
            <ul>
                <li>could customize when using database to generate</li>
                <li>support param auto complete</li>
                <li>better ui from qq group user</li>
                <li>add support for spring could recognize mapper mapperScan annotation ect</li>
            </ul>
    </p>
    <p><h4>1.8.3</h4>
            <ul>
                <li>generate testcase by one click</li>
                <li>still show database when can't connect</li>
                <li>offline activation support</li>
                <li>unbind support</li>
                <li>fix no need to focus on table to use mybatis generator</li>
                <li>other bug fix</li>
            </ul>
    </p>
    <p><h4>1.8.2</h4>
            <ul>
                <li>fix mysql using mybatis generator xml using database name</li>
            </ul>
    </p>
    <p><h4>1.8.1</h4>
            <ul>
                <li>add database support for sqlserver and oracle 10g and mysql8.0</li>
                <li>fix BaseColumnList duplicate generate</li>
                <li>fix update when xml has comments</li>
                <li>using project scope instead of module scope</li>
                <li>support annotation like insertProvider ect</li>
            </ul>
    </p>
    <p><h4>1.8.0</h4>
            <ul>
                <li>support extend on resultMap</li>
                <li>add database support oracle and postgresql</li>
                <li>better ui for using mybatis generator on database</li>
                <li>import param class</li>
                <li>fix possible bug</li>
            </ul>
    </p>
    <p><h4>1.7.9</h4>
            <ul>
                <li>bug fix</li>
            </ul>
    </p>
    <p><h4>1.7.8</h4>
            <ul>
                <li>fix qq group id</li>
                <li>bug fix</li>
            </ul>
    </p>
    <p><h4>1.7.7</h4>
            <ul>
                <li>could jump direct from java class to mapper</li>
                <li>add param annotation for mybatis mapper</li>
                <li>update charset to uft8mb4</li>
                <li>fix findByLike problem</li>
            </ul>
    </p>
    <p><h4>1.7.6</h4>
            <ul>
                <li>mybatis generator using database comment</li>
                <li>fix error when generate mybatis generator xml file</li>
                <li>fix use project scope when user use mybatis generator</li>
                <li>support when one mapper to multiple xml</li>
            </ul>
     </p>
    <p><h4>1.7.5</h4>
            <ul>
                <li>remember user config path</li>
                <li>add keymap to jump from java to xml and xml to java</li>
                <li>user could config using project or module search scope</li>
                <li>fix encoding problem when using with mybatis generator</li> </ul>
     </p>
    <p><h4>1.7.4</h4>
            <ul>
                <li>xml not find in method using warn instead of error</li>
                <li>support add jdbcType when update java class field</li>
                <li>generate mybatis generator file one click</li>
                <li>fix like problem</li>
            </ul>
     </p>
    <p><h4>1.7.3</h4>
            <ul>
                <li>fix thread assertion bug</li>
                <li>mybatis generate not change dao file</li>
                 <li>fix java dateTime jdbcType</li>
            </ul>
     </p>
    <p><h4>1.7.2</h4>
            <ul>
                <li>fix inspection for check mybatis xml not used</li>
            </ul>
     </p>
    <p><h4>1.7.1</h4>
            <ul>
                <li>support bind on mac address on device register</li>
                <li>fix order by with multiple field</li>
                <li>fix display probelm on mac when generate files</li>
                <li>fix exception on intellij on 1.7.3</li>
                <li>add override when generate service impl</li>
                <li>add scroll panel for generate by datasource</li>
                <li>delete multiple unused xml fast</li>
            </ul>
     </p>
    <p><h4>1.7.0</h4>
            <ul>
                <li>generate service add override annotation</li>
                <li>find first n return list</li>
                <li>import java class package when generate service interface</li>
            </ul>
     </p>
    <p><h4>1.6.9</h4>
            <ul>
                <li>better method name auto complete</li>
                <li>fix connect to sql database</li>
                <li>fix jdbcType for long</li>
                <li>better way to choose package</li>
                <li>find one not generate on limit</li>
                <li>support using transient</li>
            </ul>
     </p>
    <p><h4>1.6.8</h4>
            <ul>
                <li>fix icon in xml miss</li>
                <li>support more from field comment</li>
                <li>support change icon</li>
                <li>generate with jdbcType</li>
            </ul>
     </p>
    <p><h4>1.6.7</h4>
            <ul>
                <li>fix bug service interface import page</li>
                <li>could generate comment from field comment</li>
                <li>use better icon</li>
                <li>support language like updateIncVersion</li>
            </ul>
     </p>
    <p><h4>1.6.6</h4>
            <ul>
                <li>fix bug when generate method xml in service</li>
            </ul>
     </p>
    <p><h4>1.6.5</h4>
            <ul> 
                <li>support findWithPage</li>
                <li>support to configure mapper prefix</li>
            </ul>
     </p>
    <p><h4>1.6.4</h4>
            <ul>
                <li>support sqlite</li>
                <li>oracle support multiple column index,multiple column unique</li>
            </ul>
     </p>
    <p><h4>1.6.0</h4>
            <ul>
                <li>support generate if test</li>
                <li>support generate in service and service interface</li>
                <li>support multiple column index,multiple column unique</li>
                <li>support generate on function</li>
                <li>support generate dto when find more than one field</li>
                <li>not using pojo as default param</li>
            </ul>
     </p>
    <p><h4>1.4.5</h4>
            <ul>
                <li>support with enum type</li>
            </ul>
     </p>
    <p><h4>1.4.4</h4>
            <ul>
                <li>fix exception when start up</li>
            </ul>
     </p>
    <p><h4>1.4.3</h4>
            <ul>
                <li> support multiple method xml generate</li>
                <li> support for mybatis plus</li>
                <li> support domain class with protected field and static field</li>
                <li> support for small resolution</li>
                <li>bugfix - fix can't generate to path</li>
            </ul>
     </p>
    <p><h4>1.4.2</h4>
            <ul>
                <li>bugfix - fix Could not initialize class com.ccnode.codegenerator.freemarker.TemplateUtil</li>
            </ul>
     </p>
    <p><h4>1.4.1</h4>
            <ul>
                <li>bugfix - oralce insertList</li>
                <li>bugfix - import issue</li>
            </ul>
     </p>
    <p><h4>1.4</h4>
            <ul>
                <li>add support for oracle</li>
                <li>config use generate key</li>
                <li>auto complete for resultMap,refid,keyProperty,property</li>
                <li>support with java.sql.Timestamp java.sql.Date java.sql.Time Enum LocalDateTime LocalDate</li>
                <li>support update field with insertSelective</li>
                <li>add new icon of mybatis jump to xml ect</li>
            </ul>
     </p>
    <p><h4>1.3</h4>
            <ul>
                <li>add index column and hasDefault column when generate mybatis files</li>
                <li>jump from refid resultMap to their definition in mybatis xml. could refactor as well</li>
                <li>could refactor method name in xml</li>
                <li>add insertSelective when generate mybatis files</li>
                <li>generate for greaterThanOrEqualTo and lessThanOrEqualTo and betweenOrEqualTo</li>
                <li>add configuration to use with @Mapper</li>
                <li>fix not null issue for find module - bug fix</li>
            </ul>
     </p>
     <p><h4>1.2</h4>
            <ul>
                <li>add support for unsigned type, small int.</li>
                <li>check for using object type instead of primitive type</li>
                <li>support more auto completion for sql</li>
                <li>double type support - bug fix</li>
                <li>update field exception -bug fix</li>
            </ul>
     </p>

