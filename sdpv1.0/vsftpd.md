# Sdp组件之vsftpd服务

Sdp更新代码有两种方法，svn、ftp。

当前版本只能任选一种。

对于ftp选项，只能采用vsftpd，部署方式是sdp/components/vsftpd.sh，执行如下：

```sh vsftpd.sh test 123456```

如果你已经有了vsftpd，需要更新sdp/global.func文件以下全局变量：
```
export vfu="/etc/vsftpd/vfu.list"

export vfudb="/etc/vsftpd/vfu.db"

export vfudir="/etc/vsftpd/vfu_dir"```



