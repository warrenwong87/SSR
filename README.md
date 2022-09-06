关于脚本 shadowsocksR.sh：

一键安装 ShadowsocksR 服务器； 支持自定义配置：服务器端口：自己设定（如不设定，默认从 9000-19999 之间随机生成）；密码：自己设定（如不设定，默认为 teddysun.com）；加密方式：自己设定（如不设定，默认为 aes-256-cfb）；协议（Protocol）：自己设定（如不设定，默认为 origin）；混淆（obfs）：自己设定（如不设定，默认为 plain）。 ShadowsocksR(SSR) 一键安装脚本支持系统包括 CentOS 6+，Debian 7+，Ubuntu 12+。

3、脚本使用 在 VPS 上依次执行以下命令：

centos 系统安装 Curl 方法: yum update -y && yum install curl -y yum -y install wget

wget --no-check-certificate https://raw.githubusercontent.com/warrenwong87/SSR/main/shadowsocksR.sh chmod +x shadowsocksR.sh ./shadowsocksR.sh 2>&1 | tee shadowsocksR.log 之后会需要你手动输入 SSR 服务器信息，包括密码、端口、加密方式、协议、混淆，如果不设置，脚本会有默认值（具体参考上一部分的脚本介绍）：

ShadowsocksR 脚本

设置好配置后，脚本会一键安装 SSR 服务器端，等待安装完成后，提示如下：

Congratulations, ShadowsocksR server install completed! Your Server IP :your_server_ip Your Server Port :your_server_port Your Password :your_password Your Protocol :your_protocol Your obfs :your_obfs Your Encryption Method:your_encryption_method

Welcome to visit:https://shadowsocks.be/9.html Enjoy it!

4、脚本其他设置 1.脚本卸载

一键卸载 SSR 服务器以及配置文件：

./shadowsocksR.sh uninstall 2.脚本使用命令与配置文件

启动：/etc/init.d/shadowsocks start 停止：/etc/init.d/shadowsocks stop 重启：/etc/init.d/shadowsocks restart 状态：/etc/init.d/shadowsocks status

配置文件路径：/etc/shadowsocks.json 日志文件路径：/var/log/shadowsocks.log 代码安装目录：/usr/local/shadowsocks 3. SSR 多用户配置

如果需要配置 SSR 多用户，那么需要修改配置文件 /etc/shadowsocks.json，示例如下，下面的配置文件表示有3个用户，port_password 对应的是3个用户的端口和密码，修改完配置文件后，用 /etc/init.d/shadowsocks restart 命令重启 SSR 服务端生效：

{ "server":"0.0.0.0", "server_ipv6": "[::]", "local_address":"127.0.0.1", "local_port":1080, "port_password":{ "8989":"password1", "8990":"password2", "8991":"password3" }, "timeout":300, "method":"aes-256-cfb", "protocol": "origin", "protocol_param": "", "obfs": "plain", "obfs_param": "", "redirect": "", "dns_ipv6": false, "fast_open": false, "workers": 1 }
