# devpi常用指令

devpi包含三个组件：

* devpi-server：运行在服务器上，提供镜像与缓存功能
* devpi-web：提供简单界面与查询功能
* devpi-client：客户端程序，提供上传下载等功能

#### 安装devpi-server（使用docker部署就不再需要单独安装，可以在这里查看常用指令）

```
pip install -q -U devpi-server
```

验证是否安装成功，如果成功会显示版本号

```
devpi-server --version
```

开启服务器进程（init只有在第一次启动时需要）

```
devpi-server --start --init
```

默认的端口号为3141，所以现在你可以在这里查看服务器界面

[http://localhost:3141](http://localhost:3141)

安装第一个包（以simplejson为例，注意这里是服务器安装包，下面有客户端安装包的指令）

```
pip install -i http://localhost:3141/root/pypi/+simple/ simplejson
```

安装成功后卸载

```
pip uninstall -y simplejson
```

查看服务器运行状态和日志

```
devpi-server --status
devpi-server --log
```

设置当仓库中不存在包时，从豆瓣（或者国内其他源）下载包缓存到本地，默认是官方源

这里的alice/dev是用户创建的目录，下文有介绍

```
devpi index alice/dev mirror_url="http://pypi.doubanio.com/simple/"
```

关闭服务器

```
devpi-server --stop
```

#### 安装devpi-web

```
pip install -q -U devpi-web
```

使用搜索功能（以搜索devpi-client为例）

```
pip search --index http://localhost:3141/root/pypi/ devpi-client
```

定制devpi web首页，修改site-packages/devpi\_web/templates/root.pt

#### 安装devpi-client

```
pip install -U --pre -q devpi-client
```

连接到服务器（如果在启动时修改了端口号，这里要对应修改），指向根目录

```
devpi use http://localhost:3141
devpi use root/pypi
```

登录并设置root账户密码（初始密码都为空），最后登出

```
devpi login root --password ''
devpi user -m root password=123
devpi logoff
```

注册新账户和新目录，并且使用它，使用不恰当的索引可能会找不到所需的包

```
devpi user -c alice password=456
devpi login alice --password=456
devpi index -c dev bases=root/pypi
devpi use alice/dev
```

使用客户端安装包，然后验证是否安装成功

```
devpi install pytest
py.test --version
```

更多指令请参见官网文档

[https://devpi.net/docs/devpi/devpi/latest/+d/index.html](https://devpi.net/docs/devpi/devpi/latest/+d/index.html)

