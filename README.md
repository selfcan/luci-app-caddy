# luci-app-caddy

项目地址：https://github.com/caddyserver/caddy

没有添加caddy二进制程序，需要下载或编译对应cpu架构的二进制程序手动上传至路由器，然后填写对应的程序路径。

------------------------------------------------------
编译的大概步骤：抄自网上的方法
```shell
apt update
apt install xcaddy git libnss3 upx-ucl
```shell

不能安装xcaddy的可以
```shell
go install github.com/caddyserver/xcaddy/cmd/xcaddy@latest
```shell

```shell
#下载安装go
wget https://go.dev/dl/go1.21.6.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.21.6.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin

#编译  需要什么插件自行添加了 以下只添加了caddy-webdav和caddy-cgi
GOOS=linux GOARCH=mipsle GOMIPS=softfloat ~/go/bin/xcaddy build \
    --with github.com/mholt/caddy-webdav \
    --with github.com/aksdb/caddy-cgi/v2 

#编译出来可能体积很大 可以使用upx压缩一下
upx --lzma --best caddy
```shell

--------------------------------------------------------
### UI预览 ###
我只是用来做文件服务器，所以也就一般配置
![](./Image/普通启动.png)

其他功能可以自行修改编辑配置文件
![](./Image/自定义启动.png)
