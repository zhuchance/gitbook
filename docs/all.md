
#  **Sdp官方文档库**

## **stable-v1.0(sdp.sh)原理：**
1. 
泛解析一个域名(eg:*.saintic.com)到PaaS主服务器，容器即服务，所有的docker建立在分布式存储上，建立统一的数据仓库。
  
2. 
WEB型应用会生成一个包含用户名的三级域名，用户自己的域名cname到我们生成的域名上，由nginx反向代理提供一对一http路由映射到真正的docker容器上，提供FTP svn git(暂不支持)任意一种方式文件，代码上传功能，这样一个简单的PaaS。

3. 
APP型应用提供IP+PORT，并开放iptables，供用户远程应用。
  
4. 
所有关键文件均保存为JSON格式文件，由tools目录下的工具读取相应文件进行相应后续更新服务、邮件提醒等操作。

5. 
spmc:Sdp PaaS Manager Console,WEB文件，可随意放到支持PHP环境站点下或单独建个站点，以便通过网页形式创建和更新用户，支持PC端和移动端。
建议用Jenkins持续集成。

简单结构图：
![](sdp.sh.png)


## **Directory description:**
**Version1.0, Sdp**

components:PaaS基础服务器，文件服务、容器服务。

boot:引导不同类型服务创建，引导用户生成、创建IP:PORT记录，触发文件服务功能，触发容器创建及分配和限制；

builds:创建容器中主要服务，提供PaaS应用；

tools:其他工具类脚本，如续费功能、服务到期邮件提醒功能等；

spmc:Sdp持续集成简易管理控制台，创建更新用户信息。


**Version2.0, SPC**
开发中……

## **PaaS:**
*Sdp定位是一个简单PAAS平台，旨在构建简单方便快捷的PAAS云。*

Sdp1.0局限性很大，尚只支持单机环境，自由度低，适用于个人用户；
Sdp2.0(SPC)完全分布式环境、大规模部署，自由度高，适用于组织及企业级应用。

 
*以下简单说说PaaS的功能：*

PaaS改变了传统的应用交付模式，促进了分工的进一步专业化，解耦了开发团队和运维团队。
![](imgs/PAASchange.jpg)


结束语：
不论是大型企业，中小企业，软件开发商，软件供应商、运营商，还是开发和运维人员，都需充分认识到PaaS的战略核心地位和即将带来的变化，做好充分的准备，迎接PaaS时代的到来。




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


