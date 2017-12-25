PyPI是Python程序员必备工具，架设私有PyPI可以更加方便快捷地下载包

目前有三种比较主流pip私有源搭建方案

## PyPIserver

是一个体积小、使用简单、功能较少、年代久远的解决方案

详情参见此链接[https://pypi.python.org/pypi/pypiserver](https://pypi.python.org/pypi/pypiserver)

功能：

1. PyPI代理镜像
2. 单元测试

## devpi

是一个功能比较完善、体积适中、起步于2013年，到2017年末仍在不断更新的解决方案

详情参见此链接[https://devpi.net/docs/devpi/devpi/4.3/+d/index.html](https://devpi.net/docs/devpi/devpi/4.3/+d/index.html)

1. PyPI代理镜像
2. 单元测试
3. 系统测试
4. 本地缓存
5. 集成Jenkins

devpi包含三个组件：

* devpi-server：运行在服务器上，提供镜像与缓存功能
* devpi-web：提供简单界面与查询功能
* devpi-client：客户端程序，提供上传下载等功能

## Warehouse

被誉为“ 下一代PyPI ”，是最新的解决方案

除了具有以上功能之外，还具有更美观更现代的界面，同时体积庞大

虽然GitHub上更新十分活跃，但目前还没有发布正式版本

详情参见此链接[https://warehouse.readthedocs.io/development/getting-started/\#viewing-warehouse-in-a-browser](https://warehouse.readthedocs.io/development/getting-started/#viewing-warehouse-in-a-browser)

在考虑了体积、功能、稳定性、可行性后

笔者最后选择了**devpi**作为最终的解决方案！

