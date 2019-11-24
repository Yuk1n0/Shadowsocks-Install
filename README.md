# Auto Install Server Shell Script

- Intro: Auto Install Proxy Server
- System Requirement: CentOS 6+，Debian 7+，Ubuntu 12+

## How to install server:
``` bash
wget --no-check-certificate https://raw.githubusercontent.com/Yuk1n0/Shadowsocks-Install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```
**How to uninstall server**
``` bash
./shadowsocks-all.sh uninstall
```
**How to upgrade server (only support shadowsocks-libev now)**
```bash
./shadowsocks-all.sh upgrade
```
****

**How to start | stop | restart your server**

Shadowsocks-Python：
/etc/init.d/shadowsocks-python start | stop | restart | status

ShadowsocksR：
/etc/init.d/shadowsocks-r start | stop | restart | status

Shadowsocks-Go：
/etc/init.d/shadowsocks-go start | stop | restart | status

Shadowsocks-libev：
/etc/init.d/shadowsocks-libev start | stop | restart | status

****
**Configuration Files**

Shadowsocks-Python :
/etc/shadowsocks-python/config.json

ShadowsocksR ：
/etc/shadowsocks-r/config.json

Shadowsocks-Go ：
/etc/shadowsocks-go/config.json

Shadowsocks-libev ：
/etc/shadowsocks-libev/config.json

****

**Ciphers（Python and libev）:**
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

**Ciphers（Go）:**
aes-256-cfb
aes-192-cfb
aes-128-cfb
aes-256-ctr
aes-192-ctr
aes-128-ctr
chacha20-ietf

**ciphers（none means unencrypted，ShadowsocksR）:**
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

**Protocols（Only ShadowsocksR）:**
origin
verify_deflate
auth_sha1_v4
auth_sha1_v4_compatible
auth_aes128_md5
auth_aes128_sha1
auth_chain_a
auth_chain_b

**Obfs（Only ShadowsocksR ）:**
plain
http_simple
http_simple_compatible
http_post
http_post_compatible
tls1.2_ticket_auth
tls1.2_ticket_auth_compatible
tls1.2_ticket_fastauth
tls1.2_ticket_fastauth_compatible
