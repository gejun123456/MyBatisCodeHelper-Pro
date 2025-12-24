## Using Templates to Generate Code

### Starting from version 2025.1.1, EasyCode-MybatisCodeHelper will switch to a freemium model. Only template code hint functionality will require payment; other features such as preview and code generation will remain free.

### For users with customization needs, such as adding company-specific comments or using internal frameworks, template-based code generation is recommended.

### Install EasyCodeMybatisCodeHelper(1.4.0) plugin for template generation [Download Link](https://plugins.jetbrains.com/plugin/13847-easycode-mybatiscodehelper)

## Features: template code hints, real-time preview, direct IDEA editor template operations, multiple group configuration, and direct code generation from templates. The most convenient template code generation plugin.

Video tutorial: https://www.bilibili.com/video/BV19C4y1Y7RN

GitHub: https://github.com/gejun123456/EasyCodeMybatisCodeHelperTemplates - download template files
Copy template files directly to your project's easyCode directory or Scratches And Consoles' /extensions/EasyCode for code generation. Includes code hints, real-time preview, and direct template editing in IDEA editor.

Template preview:    
![scratchGenerate](https://images.brucege.com/scrachGenerate.gif)

Generate code from database tables in IDEA (multiple table selection supported):
![generateFromScratch](https://images.brucege.com/generateFromScratch.png)

Currently supports code generation from either the project's easyCode directory or the scratch directory's /extensions/EasyCode

The project's easyCode directory is recommended as it can be version controlled with git and shared with teammates to prevent loss.


### What is group.json for?  
group.json configures relationships between templates, globalConfig, and typeMapper through group names in JSON. A project can have multiple generation groups.

### New to Template Writing?  
Templates use Velocity syntax. Documentation: https://velocity.apache.org/. Contact me for template-related issues.

## Upgrade Notice  
Due to storage changes in version 1.2.8, when upgrading from pre-1.2.7 versions, export templates to JSON first, then upgrade and import the JSON.

## Template-Generated Code Has Joined Columns Without Commas  
In IDEA 2023.1's Velocity upgrade, change $velocityHasNext to $foreach.hasNext

### Empty projectPath  
For projects with parallel modules without a main project, set projectPath in mybatisCodeHelper.vm:  
```velocity
#set($projectPath="D:/workspace/idea/XXModule")
```

## GenerateCode(old) vs GenerateFromEasyCodeFolder(new)  
GenerateCode(old) uses settings-configured templates and configurations.  
GenerateFromEasyCodeFolder(new) generates from easyCode folder templates.  
GenerateFromEasyCodeFolder(new) is recommended as it provides code hints, real-time preview, direct editing, and git integration.

## Template Code Hints
Click "Add dependency for code completion" at template top for automatic dependency addition.  
This enables code hints while editing. Remove dependency when done.

## Why Package Names and Paths in mybatisCodeHelper.vm?
This approach facilitates git version control and team sharing without individual configuration.  
Future updates will enable template-file comparison and add auto-suggestions for paths and package names.

## Template Examples
#### Remove Table Name Prefix 
Edit mybatisCodeHelper.vm in globalconfig:
```velocity
#if($tableInfo.obj.name.startsWith("table_"))
$!tableInfo.setName($tableInfo.name.substring(5))
#end
```

Or define a variable:
```velocity
#set($entityName=$tableInfo.name)
#if($tableInfo.obj.name.startsWith("table_"))
#set($entityName=$tableInfo.name.substring(5))
#end
```
Use ${entityName} in templates. Multiple templates can reference this variable.

#### Add Entity Class Suffix
```velocity
#set($entityName=$tableInfo.name)
#set($entityName = $tool.append($entityName,'Entity'))
```
Use ${entityName} in templates.

#### Remove Field Prefix
Edit mybatisCodeHelper.vm in globalconfig:
```velocity
#set($removeColumnPrefix="f_")
#foreach($column in $tableInfo.fullColumn)
#if($column.obj.name.startsWith($removeColumnPrefix))
$!column.setName($tool.firstLowerCase($column.getName().substring(1)))
#end
#end
```

#### Remove Specific Insert Columns
Edit your XML template (e.g., insertBatch):
```xml
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

#### Add jdbcType and typeHandler
Edit mybatisCodeHelper.vm in globalconfig:
```velocity
#if($tool.newHashSet("java.lang.String").contains($column.type))
    #set($jdbcType="VARCHAR")
    #elseif($tool.newHashSet("java.lang.Integer","int").contains($column.type))
    #set($jdbcType="INTEGER")
    #else
    ##other types
    #set($jdbcType="VARCHAR")
#end
$tool.call($column.ext.put("jdbcType", $jdbcType))
```
Then use in XML (ext is a map for custom properties):
```xml
#{$!{column.name},jdbcType=$!{column.ext.jdbcType}}
```

#### Get Table Name, Field Name, Field Type, Schema Name
```velocity
Table name = tableInfo.obj.name
Field name = column.obj.name
Field type = $!tool.getField($tableInfo.fullColumn.get(0).obj.dataType, "typeName")
Field Java type = column.type
Schema name = ${tableInfo.obj.getParent().getName()}
```
#### more documents：
https://gejun123456.github.io/EasyCode-Plus/

### Note: EasyCodeMybatisCodeHelper plugin is forked from https://github.com/makejavas/EasyCode, modified for MybatisCodeHelperPro compatibility and direct template-based code generation.
