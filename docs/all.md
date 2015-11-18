
#  ** 纵览-部署**


## 一：Sdp

即Simple Docker PaaS,目前版本是1.0，版本地址是https://github.com/staugur/Sdp。

它目前版本是一个在固定环境的单机上部署的一套小型PaaS平台，支持nginx、httpd、tomcat、mysql、mongodb、redis、memcached服务；遗憾的是无法通过网页申请资源、管理、审计等。


## 二：要求及使用


**1.系统要求**

  由于是单机部署，并且开发的时候是以个人服务器为环境的，所以切换服务器有如下硬性要求：
  
  >1.服务器本身有Nginx服务，可参照https://github.com/staugur/CoreWeb；
  
  >2.硬件架构是CentOS6.5 x86_64位以上，要求满足docker最低安装需求；
  
  >3.存在标签为staugur/centos的容器，下载链接：
https://software.saintic.com/core/docker/staugur.tar；或通过docker pull staugur/centos下载；后期通过build构建；

  >4.仅支持iptables，如果为firewalld类型，请关闭firewalld并开启iptables；
  
  >5.软件包：jq、mailx、subversion、python

**2.安装文档**

  提示：以下安装是基于拥有一定基础水平Linux(CentOS)人员进行的。
  1.) yum –y install subversion mailx

  2.) svn co https://github.com/staugur/Sdp/tags/stable-0.1 sdp

  3.) cd sdp ; ls
  ![](imgs/sdp1.0.png)

  4.) cd components            //运行此三个脚本安装docker、httpd+svn、vsftpd服务；

  5.) sh docker.sh ; sh svn.sh ; sh vsftpd.sh sdptest 123456  //确保中间没有报错,启动服务。

  6.) svn co https://github.com/staugur/CoreWeb/tags/v1.0.0 coreweb ; cd coreweb ; sh index.sh     //如下图，根据提示输入，输入数字1安装nginx。
  ![](imgs/nginx.png)

  7.) 修改nginx、httpd监听地址或端口，其中需要nginx反向代理httpd+svn接受请求。

  8.) 具体文章请关注更新文档。

**3.使用文档**
  1. cd sdp;
  2.sh start.sh arg1 arg2 arg3 arg4 arg5
  ![](imgs/start.png)
 
Sdp以start.sh脚本开始，此脚本需要五个参数，分别是user(用户) use_time(使用时间，单位月) service_type(服务) file_type(文件类型) email(用户邮箱)。

*要求：*

1).用户名不冲突，同个用户需要多个服务当前版本必须多次以不同user执行；

2).使用时间不限，至少1个月(当前版本并不限制此值为0)；

3).服务类型：nginx、httpd、tomcat、mysql、mongodb、redis、memcached;

4).文件类型：若为web类型可支持ftp、svn，若为app类型默认无；

5).邮件提醒：部署成功后会发给用户一封信息邮件(确保不在垃圾邮件中)，大致内容包括用户名、密码、验证邮箱、服务类型，若为web服务类型则包含域名信息，否则为IP+PORT信息，若文件类型是svn则包含用户版本库地址，否则为FTP地址，最后是FAQ链接，此链接详细讲解用户应该如果使用邮件的信息。
 ![](imgs/email.png)

3.可以直接在web端访问触发，代码目录是spmc，将整个spmc目录复制到nginx网站根目录下或者单独建立虚拟主机，并修改exec.php中的密码部分：将password改为你服务器root密码，并将nginx或Apache、php-fpm的用户改为一个单独的用户，比如www，授予www无密码sudo权限。
  ![](imgs/sudo.png)
 
Spmc界面如下(建议此界面web加密访问)：
  ![](imgs/spmc.png)

##三：联系我们
Sdp为开源项目，诚请兴趣开发者；若用于商业目的请联系我们，否则将追究法律责任！

QQ：1663116375

QQ群：421353290

Phone：18201707941

E-mail：staugur@saintic.com  或  staugur@vip.qq.com

旺旺：名道staugur

