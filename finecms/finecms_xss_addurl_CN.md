# finecms xss漏洞

这里的软件版本是 finecms v5.4.0

![](Untitled-fee1ab5c-9717-409c-879d-d8db8dfa4c2b.png)

在插件模块存在一个xss漏洞，访问url为本地环境的127.0.0.1/admin.php

![](Untitled-f0f77eed-4549-4e02-ab7f-9836d314aba5.png)

点击添加，插入一个url规则，里面写入xss的payload

![](Untitled-53bb0fcc-d58f-44f6-9683-4048a1a5fcf7.png)

保存后访问插件页面，出现了xss的弹窗

![](Untitled-6d5a2968-52c2-4b4a-851f-bf85dd536069.png)

然后进行一下问题在代码中的定位

在点击添加按钮时抓包

![](Untitled-2d00bf05-4014-41a6-b7c8-85425eaa5ea8.png)

访问的是admin中的urlrule的add，对应的是dayrui/controllers/admin下的urlrule.php文件

![](Untitled-287b0365-c9ca-46c7-8df2-5fe3381b04bf.png)

对应的add函数

![](Untitled-fb5786db-9979-4d69-8866-2d0928776171.png)

发现这里没有对post中获取到的name进行过滤就直接插入数据库中了导致了xss的问题