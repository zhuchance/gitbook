# 核心组件Subversion

Svn即subversion，是比较流行的开源版本管理系统；结合Apache Httpd Server可以通过web访问版本库，相应的，就可以使用httpd的SSL、验证等功能。


# Subversion部署调试



## 一：源码包


请注意，Apache需要apr、apr-util，而在后面subversion需要与APR、Apr-util版本相契合，如果Apache为2.0.x，APR版本就为0.9.x；apache为2.2.x,对应的APR版本应为1.2.x。由于subveresion-deps包里的APR是0.9.x的，因此编译svn时要删除从deps里解压出来的apr,apr-util，改而使用apache2.2里提供的。

最完美的搭配是：apr-1.2.12  apr-util-1.2.12  httpd-2.2.4.tar.gz  subversion-1.4.5.tar.gz   subversion-deps-1.4.5.tar.gz


**1>【安装apr】**

tar zxf apr-1.2.12.tar.gz

cd apr-1.2.12

./configure --enable-shared 

make && make install

**2>【安装apr-util】**

tar zxf apr-util-1.2.12.tar.gz  

cd apr-util-1.2.12

./configure --enable-shared --with-expat=builtin --with-apr=/usr/local/apr/

make && make install

**3>【安装apache】**  

tar zxf httpd-2.2.29.tar.gz
cd httpd-2.2.29  
./configure --prefix=/usr/local/apache/ --sysconfdir=/etc/httpd --enable-mods-shared=most --enable-modules=most --enable-so --enable-rewrite=shared --enable-ssl=shared --with-ssl --enable-cgi --enable-dav --with-included-apr   --with-apr=/usr/local/apr/bin/apr-1-config --with-apr-util=/usr/local/apr/bin/apu-1-config --enable-static-support --enable-charset-lite --enable-file-cache --enable-cache --enable-disk-cache --enable-mem-cache --enable-static-ab --enable-maintainer-mode --enable-deflate  --with-mpm=worker

make && make install  

cp /usr/local/apache/bin/apachectl /etc/init.d/httpd

**4>【安装subversion】**

下面这两个包会自动解压成一个包subversion-1.6.6

tar zxf subversion-1.6.6.tar.gz  

tar zxf subversion-deps-1.6.6.tar.gz   

cd subversion-1.6.6

rm -rf apr  

rm -rf apr-util

./configure --prefix=/usr/local/svn --with-apxs=/usr/local/apache/bin/apxs --with-apr=/usr/local/apr/ --with-apr-util=/usr/local/apr/ --with-ssl --with-neon --enable-shared

make && make install  


## 二：RPM包

components源代码如下：

脚本是以YUM包管理系统安装的httpd和svn，要求httpd配置目录为/etc/httpd/conf/httpd.conf，扩展配置目录为/etc/httpd/conf.d/，除非您修改sdp源码global.func，修改第十行，更改svnconf变量值。

![](imgs/svnconf.png)
 
保证可以使用/etc/init.d/httpd reload重载服务，也就是说在CentOS7或RHEL7的YUM安装方式上不适用。
默认安装中禁用了HTTPS功能，如果你有证书，可以设置Apache Httpd Server的SSL功能。

Tags标签stable即1.0默认global.func启用了SSL，如果没有那么需要将global.func中如下图断中的SSLRequireSSL前加#注释掉。

 ![](imgs/svnrepo.png)
 
之后的版本默认注释掉，如果需要开启SSL将#去掉。







