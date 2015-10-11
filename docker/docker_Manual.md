# Sdp组件之docker服务

Docker是一次革命性技术，它彻底释放了虚拟化的威力！

Sdp核心技术即docker服务：

    APP型应用每一个APP则为一个容器，每个容器开启相应端口与并设置转发；
    
    WEB型应用在宿主机端nginx设置反向代理。
    

此脚本自动安装docker服务，支持的系统是CentOS、RHEL6.5以上。
可以svn签出或git克隆一下链接脚本：
https://github.com/staugur/scripts/trunk/MyOther/docker/.docker_tools.sh
    将.docker_tools.sh放到家目录并写入到.bashrc以便每次登陆都加载此脚本。

最后sdp系统需要7大镜像，下载链接：https://software.saintic.com/core/docker/；
并将之导成镜像。




