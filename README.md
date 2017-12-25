# 搭建pip私有源

本文旨在介绍使用devpi搭建pip私有源的整个流程及相关指令

需要的工具：

* devpi：PyPI服务器和打包/测试/发布工具
* nginx：著名的Web服务器
* docker：开源的应用容器引擎

初次部署devpi，可以从Docker部署开始，然后熟悉各种常用指令

nginx用来反向代理，实现负载均衡，该功能非必选，建议先部署一台服务器观察流量再做决定

docker用来更方便的将整个环境部署任意一台机器上

本文将从上述三个方面展开具体介绍

最终实现的功能：局域网内机器可以使用如下指令方便的安装python各种库（以pytest为例）

```
pip install pytest
```

欢迎邮件交流 shixu@megvii.com

