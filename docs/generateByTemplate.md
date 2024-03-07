## 使用模版来生成代码（插件3.1.9版本）

### 部分用户有定制的需求，比如公司代码要加特定的注释等，或者用了公司内部框架等，推荐用模版来生成代码

### 安装EasyCodeMybatisCodeHelper(1.3.4)版本插件来进行模版生成 [下载地址](https://plugins.jetbrains.com/plugin/13847-easycode-mybatiscodehelper)

## 支持写模版代码提示，实时预览模版，直接在idea编辑器操作模版，可配置多个分组，直接从模版来生成代码.最方便的模版生成代码插件

视频地址: https://www.bilibili.com/video/BV19C4y1Y7RN

github:https://github.com/gejun123456/EasyCodeMybatisCodeHelperTemplates 下载模版文件
直接把模版文件拷到项目的easyCode目录或者Scratches And Consoles的/extensions/EasyCode到来生成代码，写模版有代码提示，可以实时预览模版，直接在idea编辑器操作模版 

或者可以从json导入老模版   
![importToScratch](https://images.brucege.com/importToScratch.png)

模版预览:    
![scratchGenerate](https://images.brucege.com/scrachGenerate.gif)

生成代码,在idea的数据库表上,可以选多张表生成:
![generateFromScratch](https://images.brucege.com/generateFromScratch.png)

目前支持项目的easyCode目录或者scratch目录下的/extensions/EasyCode目录进行识别生成代码

推荐使用项目的easyCode目录，可以放到git中以及和同事共享防止丢失

### 怎么从之前用设置配置的模版导入到 从easycode文件目录生成代码  
先将之前设置配置的本地导出到json，再从json导入到scratch那个，导入到scratch后 就可以直接复制easyCode文件夹到项目的根目录，
从https://github.com/gejun123456/EasyCodeMybatisCodeHelperTemplates 弄一个group.json放在easyCode目录下就可以生成代码了
![exportAndImport](https://images.brucege.com/exportAndImport.png)
![fromScratch](https://images.brucege.com/scratchTemplateGenerate.png)

### group.json 做啥用的  
group.json是配置关联关系的，模版和globalConfig和typeMapper都是多对多的关系通过配置json的group名来进行区分，一个项目可以有多个生成组

### 我不会写模版怎么办？  
模版用的是velocity语法 文档:https://velocity.apache.org/ 碰到模版问题也可联系我来弄弄

## 升级插件注意  
由于1.2.8版本对存储进行了更改，从1.2.7版本之前升级到之后的版本，需要先导出模版到json，升级到高版本然后导入json.

## 模版生成的代码column连在了一起，中间没有逗号  
2023.1 idea升级了velocity，把$velocityHasNext 改成$foreach.hasNext即可

### projectPath为空  
如果你的项目是一个多module平行的项目，没有一个总的project，可以在mybatisCodehelper.vm中将projectPath set为具体的路径  
#set($projectPath="D:/workspace/idea/XXModule")

## GenerateCode(old)和GenerateFromEasyCodeFolder(new)的区别是啥  
GenerateCode(old)老的模版是在设置里面配置的,走的是设置里面的template globalConfig等配置,  
GenerateFromEasyCodeFolder(new)是直接从easyCode文件夹下的模版生成的.  
当你使用GenerateFromEasyCodeFolder(new) 无需在设置里面配置模版，推荐使用GenerateFromEasyCodeFolder(new),  
写模版有代码提示，可以实时预览模版，直接在idea编辑器操作模版，还可以加到git中方便与同事共享

## 写模版代码提示
模版最上面有个链接 Add dependency for code completion,点击后会自动添加依赖,  
之后编辑模版会有代码提示，编辑完模版后可以remove dependency来移除依赖

## 为何包名和路径要放在mybatisCodeHelper.vm中，为啥不用ui配置路径
包名和路径放在mybatisCodeHelper.vm的好处是方便放到git中和同事共享，不用每个人都去配置  
未来也可利用这个来进行模版和已存在的文件直接对比，方便找到具体的路径,  
mybatisCodeHelper.vm的路径和包名未来会加入自动提示，方便填写  

## 模版例子
#### 移除表名前缀 
编辑globalconfig中的mybatisCodeHelper.vm
```
#if($tableInfo.obj.name.startsWith("table_"))
$!tableInfo.setName($tableInfo.name.substring(5))
#end
```

也可以定义一个变量
```
#set($entityName=$tableInfo.name)
#if($tableInfo.obj.name.startsWith("table_"))
#set($entityName=$tableInfo.name.substring(5))
#end
```
在模版中使用 ${entityName}来进行引用，多个模版可以直接引用这个变量

#### Entity类添加后缀
```
#set($entityName=$tableInfo.name)
#set($entityName = $tool.append($entityName,‘Entity’))
```
模版中使用 ${entityName}来进行引用

#### 移除字段前缀
编辑globalconfig中的mybatisCodeHelper.vm
```
#set($removeColumnPrefix="f_")
#foreach($column in $tableInfo.fullColumn)
#if($column.obj.name.startsWith($removeColumnPrefix))
$!column.setName($tool.firstLowerCase($column.getName().substring(1)))
#end
#end
```

#### insert移除部分列
编辑你的xml模版 比如insertBatch
```
    #set($insertSkipFields = ["create_time","update_time"])
    <insert id="insertBatch" keyProperty="$!pk.name" useGeneratedKeys="true">
        insert into $!{tableInfo.obj.name}
        (
#foreach($column in $tableInfo.otherColumn)
#if($insertSkipFields.contains($column.obj.name))
#elseif($foreach.hasNext)
            $!column.obj.name,
        #else
            $!column.obj.name
        #end#end
        )
        values
        <foreach collection="entities" item="entity" separator=",">
        (
#foreach($column in $tableInfo.otherColumn)
#if($insertSkipFields.contains($column.obj.name))
#elseif($foreach.hasNext)
            #{entity.$!{column.name}},
#else
            #{entity.$!{column.name}}
#end#end
            )
        </foreach>
    </insert>
```

#### 加上jdbcType typeHandler等
编辑globalconfig中的mybatisCodeHelper.vm
```
#if($tool.newHashSet("java.lang.String").contains($column.type))
        #set($jdbcType="VARCHAR")
        #elseif($tool.newHashSet("java.lang.Integer","int").contains($column.type))
        #set($jdbcType="INTEGER")
        #else
        ##其他类型
        #set($jdbcType="VARCHAR")
    #end
$tool.call($column.ext.put("jdbcType", $jdbcType))
```
然后在xml中使用,ext是一个map，可以随意添加属性，方便用户使用
```
#{$!{column.name},jdbcType=$!{column.ext.jdbcType}}
```
这种代码调用即可

#### 获取表名，字段名，字段类型，schema名
```
    表名= tableInfo.obj.name
    字段名= column.obj.name
    字段类型=$!tool.getField($tableInfo.fullColumn.get(0).obj.dataType, "typeName")
    字段java类型=column.type
    schema名=${tableInfo.obj.getParent().getName()}
```


### EasyCodeMybatisCodeHelper插件代码fork自 https://github.com/makejavas/EasyCode 插件，修改了部分代码用于兼容MybatisCodeHelperPro插件,提供了直接从模版生成代码的功能



