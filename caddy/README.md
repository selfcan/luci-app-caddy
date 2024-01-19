通过这个构建的二进制程序 不能开启webdav  会导致启动失败，而单独构建的添加了webdav模块的可以开启webdav
所以最好是单独编译
```shell
GOOS=linux GOARCH=mipsle GOMIPS=softfloat ~/go/bin/xcaddy build \
    --with github.com/mholt/caddy-webdav \
    --with github.com/aksdb/caddy-cgi/v2
```

在51行添加了upx压缩用来节省体积
```shell
$(STAGING_DIR_HOST)/bin/upx --lzma --best $(GO_PKG_BUILD_BIN_DIR)/caddy

$(STAGING_DIR_HOST)/bin/upx 对应的是编译器的 openwrt-sdk-版本-架构名_gcc-版本号_musl.Linux-x86_64/staging_dir/host/bin目录里 
如果这个目录没有这个upx  可以改为其他目录 如 /usr/bin/upx --lzma --best $(GO_PKG_BUILD_BIN_DIR)/caddy
都没有可以安装也可以下载https://github.com/upx/upx/releases二进制
```

在55-56行 
```shell
$(INSTALL_DIR) $(1)/tmp
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/caddy $(1)/tmp/caddy
```

设置安装在/tmp/caddy了 ， 如果你路由器闪存空间足够，可改为/usr/bin/caddy
```shell
$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/caddy $(1)/usr/bin/caddy
```
