# finecms xss vulnerability

The vesion of program is finecms v5.4.0

![](Untitled-fee1ab5c-9717-409c-879d-d8db8dfa4c2b.png)

There is a XSS in plugin module，my local url is '127.0.0.1/admin.php'

![](Untitled-f0f77eed-4549-4e02-ab7f-9836d314aba5.png)

click the '添加' button，insert an url rule and the name is '<script>alert(111)</script>'

![](Untitled-53bb0fcc-d58f-44f6-9683-4048a1a5fcf7.png)

Save and access the plugin page.The XSS alert appears.

![](Untitled-6d5a2968-52c2-4b4a-851f-bf85dd536069.png)

And then I will find the program location in the code.

I capture the package when I click the '添加' button in burpsuite.

![](Untitled-2d00bf05-4014-41a6-b7c8-85425eaa5ea8.png)

In url we can find admin.php and `c=urlrule m=add`，in directory is dayrui/controllers/admin/urlrule.php

![](Untitled-287b0365-c9ca-46c7-8df2-5fe3381b04bf.png)

in this file we can find the add() function

![](Untitled-fb5786db-9979-4d69-8866-2d0928776171.png)

So it's clearly that there is not filter when getting the post data 'name'.And insert a unsafe 'name' in database
