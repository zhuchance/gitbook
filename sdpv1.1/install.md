# Sdp v1.1 安装部署

建议采用我提供的一键部署环境脚本，在分支autodeploy下。

具体的脚本是：https://github.com/saintic/Sdp/branches/autodeploy

使用方法：

svn export https://github.com/saintic/Sdp/branches/autodeploy/install_sdp1.1.sh && sh install_sdp1.1.sh

如果不用一键安装方式，只要环境有docker、nginx、redis、vsftpd。

## 1.docker

参考链接：http://www.saintic.com/sdpv1.0/docker.html

部署脚本：http://www.saintic.com/blog/9.html

需要的镜像列表："mongodb", "mysql", "redis", "memcache", "nginx", "tengine", "httpd", "lighttpd", "tomcat"

首页中已提到我的docker官方仓库名是staugur，所以要pull以上镜像列表，方法如下：

docker pull staugur/image(镜像名)

如果你想自定义你的镜像，可以下载我的base镜像，centos 190M不到，docker pull staugur/base，然后修改源码中的Core/Docker.py中的volumes对应的容器WEB服务根目录。


## 2.nginx

参考LNMP文档nginx部分：http://www.saintic.com/blog/8.html

更多选择请参考另个项目：https://github.com/staugur/CoreWeb

也可以采用rpm包安装方式，官方包链接：http://nginx.org/en/linux_packages.html#stable

这部分要求sdp.cfg配置文件中的NginxProxy目录存在，且nginx.conf主配置文件包含NginxProxy代理目录，以供用户的WEB请求创建的域名访问。



## 3.redis

rpm包管理器安装

```yum -y install epel-release ; yum makecache ; yum -y install redis```

源码包安装

```请参考https://github.com/staugur/CoreWeb```

