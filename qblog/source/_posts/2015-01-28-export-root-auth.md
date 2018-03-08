---
date: 2015-01-28 18:02:12
layout: post
title: 怎么导出p12的根证书
categories: 日志
tags: ios
---

###导出根证书步骤		

步骤1 ：在LauchPad中找到“钥匙串”这个应用， 打开    

[![](/album/root_auth/root_auth_1.png)](/album/root_auth/root_auth_1.png)     

步骤2：打开的“钥匙串”应用如下，如下图，选择“登录”-“证书”，在右边找到自己的证书，（如果没有像下图展开，则单击2旁边那个三角展开），按住command键同时选中两项，右击“导出2项”。    

[![](/album/root_auth/root_auth_2.png)](/album/root_auth/root_auth_2.png)    

步骤3：保存，选择存放路径，文件格式选择.p12，选择存储   

[![](/album/root_auth/root_auth_3.png)](/album/root_auth/root_auth_3.png)    


步骤4：输入密码（该密码用于使用.p12证书的人，使用的时候需要输入密码此才能完成导入）    

[![](/album/root_auth/root_auth_4.png)](/album/root_auth/root_auth_4.png)   

步骤5：选择“好”，保存本地  


###使用p12证书		

1. 双击p12证书，输入密码（导出的时候设置密码）   

2. 重复导出步骤1，2查看证书是否存在    

