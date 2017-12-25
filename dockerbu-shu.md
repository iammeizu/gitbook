### Docker部署

Docker可以说是最近最火热的开源项目之一了，优势有这么几点。

1. 持续部署与测试：Docker在开发与运维的世界中具有极大的吸引力，因为它能保持跨环境的一致性。Docker容器通过相关配置，保持容器内部所有的配置和依赖关系始终不变。
2. 多云平台：Docker支持所有主流的云计算提供商，包括亚马逊AWS和谷歌的GCP。
3. 环境标准化和版本控制：Docker容器还可以像git仓库一样，通过不同的版本来管理Docker镜像。设想如果因为完成了一个组件的升级而导致整个环境都损坏了，Docker可以轻松地回滚到这个镜像的前一个版本。
4. 隔离性：Docker可以确保应用程序与资源是分隔开的，每个容器拥有自己的资源，并且和其他容器是隔离的。除此之外，Docker还能确保每个应用程序只使用分配给它的资源（包括CPU、内存和磁盘空间）
5. 安全性：由于Docker容器是隔离的，并且资源是受限制的，所以即使你其中一个应用程序被黑，也不会影响运行在其它Docker容器上的应用程序。

安装Docker

可以登录Docker官网下载，安装也十分简单，这里不再赘述

从云端取镜像

镜像地址[https://harbor.csg-bjv.megvii-inc.com/harbor/projects/28/repository](https://harbor.csg-bjv.megvii-inc.com/harbor/projects/28/repository)

```
docker pull harbor.csg-bjv.megvii-inc.com/devpi-shixu:v1
```

运行devpi-server

```
docker run -d -p 3141:3141 devpi-shixu:v1
```

####  {#用户手册}

有的时候通过devpi use指令没有成功修改pip源地址

那么用户需要手动修改~/.pip/pip.conf文件

把其中localhost改成服务器ip地址，端口号如果有修改也对应修改

```
[global]
index-url = http://localhost:3141/root/pypi/
```

修改完成之后就可以执行下面指令直接下载包

```
pip install pytest
py.test --version
```

如果成功查看到了版本号，恭喜你完成了配置！

