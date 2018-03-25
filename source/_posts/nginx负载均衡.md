title: nginx负载均衡
author: Halfopen
tags:
  - nginx
categories:
  - linux
date: 2018-03-25 21:12:00
---
目前要在两台机器上做负载均衡，按网上的教程写的，一般都是两台机器按一样的配置，或者就是配好后只访问一台，这里总结一下。

以机器1的9000为负载均衡端口，其他机器的8000端口访问本机

- 机器1:172.16.201.1
- 机器2:172.16.201.2

#### 172.16.201.1配置
```shell
upstream myservers{
		server 127.0.0.1:8000 weight=2;
    	server 127.0.0.2:8000 weight=1;
    		
}
server { 
    listen 8000;
    server_name 127.0.0.1; 
    
    location / { 
        这里不要写proxy_pass，以免出现互相转发死循环，转发只发生在9000端口
    }
}
server { 
    listen 9000; # 负载均衡转发端口
    server_name 127.0.0.1; 
    
    location / { 
        proxy_pass http://myservers;
    }
}
```

#### 172.16.201.2配置
```shell
server { 
    listen 8000;
    server_name 127.0.0.1; 
    
    location / { 
        这里不要写proxy_pass，以免出现互相转发死循环，转发只发生在9000端口
    }
}
```
这样访问 172.16.201.1:9000就可以按访问频率分发到两个机器上了

最好使用firefox，不要用chrome,不要打开开发者工具 


![upload successful](/assets/images/nginx负载均衡/x.gif)
