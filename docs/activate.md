# 无法进行激活
## 如果激活报密文数据已损坏或者DnsFilter.testQuery报错
请先更新到插件最新版本(qq群:575733084)版本重新激活一下
还不能解决的话请联系我微信gejun12311包搞定

请检查Intellij是否使用了ja-netfilter>=20220701版本   
最新版的ja-netfilter屏蔽了brucege.com并且不让插件进行正版验证 请打开ja-netfilter目录修改ja-netfilter\config\dns.conf  
把equal brucege.com 那一行给删掉
或者使用插件的 3.3.1版本来激活


## 如果电脑无法访问 http://brucege.com/pay/view
请联系微信gejun12311来进行离线激活，将插件离线激活里面的唯一码和购买的在线激活码发给他

## mac无法激活，Permission denied
![noPermission](https://images.brucege.com/noPermission.png)
请使用 cd ~ 然后 sudo chmod 777 .config 即可
