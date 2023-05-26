## 迁移到模版来生成代码（插件3.1.9版本）

### 部分用户有定制的需求，比如公司代码要加特定的注释等，或者用了公司内部框架等，推荐用模版来生成代码

### MybatisCodeHelperPro插件为3.1.9或以上的版本，安装EasyCodeMybatisCodeHelper(1.3.0)版本插件来进行模版生成

视频地址: https://www.bilibili.com/video/BV1dL41127SQ  

github:https://github.com/gejun123456/EasyCodeMybatisCodeHelperTemplates 下载模版文件
直接把模版文件拷到项目的easyCode目录或者Scratches And Consoles的/extensions/EasyCode到来生成代码，写模版有代码提示，可以实时预览模版，直接在idea编辑器操作模版 

或者可以从json导入老模版   
![importToScratch](https://images.brucege.com/importToScratch.png)

模版预览:    
![scratchGenerate](https://images.brucege.com/scrachGenerate.gif)

生成代码,在idea的数据库表上,可以选多张表生成:
![generateFromScratch](https://images.brucege.com/generateFromScratch.png)

目前支持项目的easyCode目录或者scratch目录下的/extensions/EasyCode目录进行识别生成代码

推荐使用项目的easyCode目录，可以放到git中和同事共享防止丢失

### EasyCodeMybatisCodeHelper插件代码fork自https://github.com/makejavas/EasyCode 插件，修改了部分代码用于兼容MybatisCodeHelperPro插件



