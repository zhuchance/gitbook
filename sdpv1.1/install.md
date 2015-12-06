# Sdp v1.1 安装部署

建议采用我提供的一键部署环境脚本，文档可参考：http://www.saintic.com/sdpv1.0/autodeploy.html

具体的脚本是：https://github.com/staugur/Sdp/branches/autodeploy

使用方法：

svn export https://github.com/staugur/Sdp/branches/autodeploy/install_sdp1.1.sh && sh install_sdp1.1.sh

如果不用一键安装方式，只要环境有docker、nginx、httpd(svn)、redis、vsftpd。


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


## 3.httpd(svn)

由于目前只支持http(s)方式的svn访问，所以subversion+httpd是有必要的。

两者部署都很简单，建议采用rpm包方式，

```yum -y install httpd svn mod_dav_svn```

方法：
```
svn export https://github.com/staugur/scripts/trunk/services/httpd+svn_easy.sh
sh httpd+svn_easy.sh
```

如果要源码安装，可参考LAMP的apache httpd部分，参考链接：http://www.saintic.com/blog/6.html

注意一定要安装apr apr-util，然后再安装svn。
```
#下面这两个包会自动解压成一个包subversion-1.6.6
tar zxf subversion-1.6.6.tar.gz  
tar zxf subversion-deps-1.6.6.tar.gz   
cd subversion-1.6.6
rm -rf apr  
rm -rf apr-util
./configure --prefix=/usr/local/svn --with-apxs=/usr/local/apache/bin/apxs --with-apr=/usr/local/apr/ --with-apr-util=/usr/local/apr/ --with-ssl --with-neon --enable-shared
make  
make install  
```

配置部分：


