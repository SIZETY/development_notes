# 解决 github 连接超时的问题

## 起因

在最开始的时候，每次在推代码的时候总是很慢，最近几次直接 timeout 无法推送，也无法拉取，尝试 clone 其它仓库也不行。

## 分析

> https://blog.csdn.net/the__future/article/details/130038818

经过搜索问题原因得到结果：确实是与 github 连接的时候超时了。

## 解决方案


**1. 先测试与 github ssh 连接状态**

```shell
$ ssh -T git@github.com
# 如果是连接成功会有成功提示
```

**2. 添加或修改 ~/.ssh/config 文件来解决**

在 ssh 的私钥和密钥的同级，创建 `config` 文件（注意名字就是 config，没有后缀），这个文件将配置 ssh 连接 github 的地址和端口，然后添加配置内容


```shell
Host github.com
HostName ssh.github.com
User git
Port 443
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
```

保存后，再次尝试。
