# 达梦数据库支持 (xml中sql自动提示和补全)

达梦数据库语法类似于oracle,

参考文章 https://blog.csdn.net/ilqgffvramusm2864/article/details/106211496

然后设置中dialect配置 oracle 参考文档配置数据库那节

上面文章中的驱动 需要改为我改过的驱动 idea会把达梦数据库识别为oracle数据库。
兼容的是oracle的语法，达梦数据库支持的非oracle语法则不能识别。

驱动下载地址:https://share.weiyun.com/mdyhnTtL, 如果有问题，请联系我

如果急用，请把方言配置为generic sql 然后使用官方的驱动
官方驱动下载地址:https://eco.dameng.com/download/


## 复杂但是代码提示更好的方案

本地弄一个 oracle，把达梦的表使用DTS工具迁移过去，然后在 oracle 的表上操作

## idea社区版 达梦数据库生成

请加入qq群516959916 里面单独支持社区版的版本

