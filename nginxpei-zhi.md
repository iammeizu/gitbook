#### Nginx负载均衡配置 {#nginx负载均衡配置}

负载均衡的目的是为了解决单个节点压力过大，造成Web服务响应过慢，甚至瘫痪无法正常提供服务。

Nginx负载均衡是通过upstream模块来实现的，内置实现了三种负载策略，配置比较简单的。

* 轮循（默认）：Nginx根据请求次数，将每个请求均匀分配到每台服务器
* 最少连接：将请求分配给连接数最少的服务器。Nginx会统计哪些服务器的连接数最少。
* IP Hash：绑定处理请求的服务器。根据客户端的IP算出一个HASH值，将请求分配到集群中的某一台服务器上。

这里使用默认的轮训机制即可

```
http {

    # ... 省略其它配置

    upstream tomcats {
        server 192.168.0.100:8080;
        server 192.168.0.101:8080;
        server example.com:8080;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://tomcats;
        }
    }

    # ... 省略其它配置
}

```

1. proxy\_pass[http://tomcats](http://tomcats/): 表示将所有请求转发到tomcats服务器组中配置的某一台服务器上。这里的tomcats可以自定义，但是必须保证上下一致。

2. upstream模块：配置反向代理服务器组，Nginx会根据配置，将请求分发给组里的某一台服务器。

3. upstream模块下的server指令：配置处理请求的服务器IP或域名，使用ifconfig可以查询到IP地址，端口可选不配置默认使用80端口。

更多内容参见官方网站文档[http://nginx.org/en/docs/http/load\_balancing.html](http://nginx.org/en/docs/http/load_balancing.html)

