# Shadowsocks 一键安装脚本(四合一)

- 脚本说明: Shadowsocks 一键安装脚本(四合一)
- 系统支持: CentOS 6+，Debian 7+，Ubuntu 12+

## 下载安装:
``` bash
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/Yuk1n0/Shadowsocks-Install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```
卸载方法
``` bash
./shadowsocks-all.sh uninstall
```

各版本启动|停止|重启|状态命令

Shadowsocks-Python 版：
/etc/init.d/shadowsocks-python start | stop | restart | status

ShadowsocksR 版：
/etc/init.d/shadowsocks-r start | stop | restart | status

Shadowsocks-Go 版：
/etc/init.d/shadowsocks-go start | stop | restart | status

Shadowsocks-libev 版：
/etc/init.d/shadowsocks-libev start | stop | restart | status

各版本默认配置文件

Shadowsocks-Python 版：
/etc/shadowsocks-python/config.json

ShadowsocksR 版：
/etc/shadowsocks-r/config.json

Shadowsocks-Go 版：
/etc/shadowsocks-go/config.json

Shadowsocks-libev 版：
/etc/shadowsocks-libev/config.json

可选 14 种加密方式的其中之一（Python 和 libev 版）
aes-256-gcm
aes-192-gcm
aes-128-gcm
aes-256-ctr
aes-192-ctr
aes-128-ctr
aes-256-cfb
aes-192-cfb
aes-128-cfb
camellia-128-cfb
camellia-192-cfb
camellia-256-cfb
chacha20-ietf-poly1305
chacha20-ietf

可选 7 种加密方式的其中之一（Go 版）
aes-256-cfb
aes-192-cfb
aes-128-cfb
aes-256-ctr
aes-192-ctr
aes-128-ctr
chacha20-ietf

可选 10 种加密方式的其中之一（none 是不加密，ShadowsocksR 版）
none
aes-256-cfb
aes-192-cfb
aes-128-cfb
aes-256-cfb
aes-192-cfb
aes-128-cfb
aes-256-ctr
aes-192-ctr
aes-128-ctr
chacha20-ietf

可选 7 种协议（protocol）的其中之一（仅限 ShadowsocksR 版）
origin
verify_deflate
auth_sha1_v4
auth_sha1_v4_compatible
auth_aes128_md5
auth_aes128_sha1
auth_chain_a
auth_chain_b

可选 9 种混淆（obfs）的其中之一（仅限 ShadowsocksR 版）
plain
http_simple
http_simple_compatible
http_post
http_post_compatible
tls1.2_ticket_auth
tls1.2_ticket_auth_compatible
tls1.2_ticket_fastauth
tls1.2_ticket_fastauth_compatible
