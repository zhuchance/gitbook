# Docker

Docker是一项伟大的技术，我有个同事曾经说过，Jenkins+Docker是手工时代的革命。

Docker的出现给DevOps注入了强大而新鲜的血液，也给PaaS带来了曙光和黎明！它的出现，被称为“云计算的下一件大事”。

GAE与GCE早已就Docker秘密研发多时，百度BAE团队早在Docker发展初期就研究了其技术，并在BAE3.0正式采用并推出了商用版，UCloud、阿里云等也对Docker进行了支持。

这意味着Docker技术将取代传统的PaaS容器技术，正式进入主流，Docker也将大幅拓宽PaaS的应用范围，隐隐有取代IaaS之势。

构建Sdp PaaS的核心组件即docker。


如果您想学习docker，推荐一个翻译Docker官网的在线文档地址：
http://dockerpool.com/static/books/docker_practice/index.html

# Sdp组件之docker服务

Docker是一次革命性技术，它彻底释放了虚拟化的威力！

Sdp核心技术即docker服务：

    1.APP型应用每一个APP则为一个容器，每个容器开启相应端口与并设置转发；
    
    2.WEB型应用在宿主机端nginx设置反向代理。
    


下载链接：https://github.com/staugur/sdp/trunk/components/docker.sh

    1.此脚本自动安装docker服务，支持的系统是CentOS、RHEL6.5、7 64Bit系统以上。

    2.可以svn export下载链接，其中一段代码是docker_tools，自动保存到~/.bashrc以便每次登陆都加载此脚本。

简单介绍一下其中的几个实用的docker命令：

    docker-enter,进入容器内，参数为container id；
    docker-pid，参看容器PID，参数为container id;
    docker-ip，查看容器IP，参数为container id。
    
顺便提一下，如果你需要固定容器IP，请参考我另一个小项目：

    https://github.com/staugur/fix_docker_ip


需要下载七大Docker image并将之导入到本地镜像库中，下载链接：https://saintic.top/docker


导入方法参见：
http://dockerpool.com/static/books/docker_practice/container/import_export.html





