# Sdp v1.1 使用手册

```
├── Core
│   ├── Core.py
│   ├── Docker.py
│   ├── __init__.py
│   ├── Mail.py
│   ├── Nginx.py
│   ├── Public.py
│   └── Redis.py
├── README.md
├── sdp.cfg
└── start.py
```

**运行**

```python start.py```

Usage:user time service email

需要传入四个参数，分别是用户名、使用时间、服务类型、用户邮箱。

用户名要求以英文字母或\_开头加上英文或数字或\_至少两位；

使用时间要求正整数，代表月份，至少为1；

服务类型定义在Core/Public.py，分为APP型和WEB型，WEB型默认使用ftp；

用户邮箱必须匹配正则验证。

如果在使用中遇到任何问题，欢迎提出，地址是[https://github.com/SaintIC/Sdp/issues](https://github.com/SaintIC/Sdp/issues)