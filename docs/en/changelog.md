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

