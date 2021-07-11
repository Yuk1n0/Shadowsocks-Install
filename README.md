# Auto Install Server Shell Script

- Intro: Auto Install Proxy Server
- System Requirement: CentOS 6+，Debian 7+，Ubuntu 12+

## How to install server:
``` bash
wget --no-check-certificate https://raw.githubusercontent.com/Yuk1n0/Shadowsocks-Install/master/shadowsocks.sh
chmod +x shadowsocks.sh
./shadowsocks.sh 2>&1 | tee shadowsocks.log
```
**How to uninstall server**
``` bash
./shadowsocks.sh uninstall
```
**How to upgrade server (only support shadowsocks-libev now)**
```bash
./shadowsocks.sh upgrade
```
****

**How to start | stop | restart your server**

Shadowsocks-libev：
/etc/init.d/shadowsocks-libev start | stop | restart | status

ShadowsocksR：
/etc/init.d/shadowsocks-r start | stop | restart | status

****
**Configuration Files**

Shadowsocks-libev ：
/etc/shadowsocks-libev/config.json

ShadowsocksR ：
/etc/shadowsocks-r/config.json

****

**Ciphers（Shadowsocks-libev）:**
aes-256-gcm
aes-192-gcm
aes-128-gcm
aes-256-cfb
aes-192-cfb
aes-128-cfb
aes-256-ctr
aes-192-ctr
aes-128-ctr
camellia-256-cfb
camellia-192-cfb
camellia-128-cfb
xchacha20-ietf-poly1305
chacha20-ietf-poly1305
chacha20-ietf
chacha20
salsa20
bf-cfb
rc4-md5

**Ciphers（none means unencrypted，ShadowsocksR）:**
none
aes-256-cfb
aes-192-cfb
aes-128-cfb
aes-256-cfb8
aes-192-cfb8
aes-128-cfb8
aes-256-ctr
aes-192-ctr
aes-128-ctr
chacha20-ietf
xchacha20
xsalsa20
chacha20
salsa20
rc4-md5

**Protocols（Only ShadowsocksR）:**
origin
verify_deflate
auth_sha1_v4
auth_sha1_v4_compatible
auth_aes128_md5
auth_aes128_sha1
auth_chain_a
auth_chain_b
auth_chain_c
auth_chain_d
auth_chain_e
auth_chain_f

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
