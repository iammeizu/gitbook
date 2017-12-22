# 搭建pip私有源

写给想要搭建私有源的各位python程序员

需要的工具：

* devpi：PyPI服务器和打包/测试/发布工具
* nginx：著名的Web服务器
* docker：开源的应用容器引擎

至于为什么选择devpi，参见[https://www.gitbook.com/book/lanrenxu/-pip/details](https://www.gitbook.com/book/lanrenxu/-pip/details)

nginx用来反向代理，实现负载均衡，该功能非必选

docker用来更方便的将整个环境部署任意一台机器上，

本文将从上述三个方面展开具体介绍

最终实现的功能：局域网内每台机器都可以使用如下指令方便的安装python各种库（以pytest为例）

```
pip install pytest
```



