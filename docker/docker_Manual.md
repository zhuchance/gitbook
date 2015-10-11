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





