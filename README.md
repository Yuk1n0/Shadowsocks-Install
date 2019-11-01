# 一键安装脚本(四合一)

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

# BBRplus 

## 脚本安装方法：  

一键脚本（全系统）：   
参见https://github.com/chiakge/Linux-NetSpeed   

一键脚本（仅CentOS）：  
```bash
wget --no-check-certificate https://raw.githubusercontent.com/Yuk1n0/Shadowsocks-Install/master/bbrplus_centos.sh && chmod +x bbrplus_centos.sh && ./bbrplus_centos.sh
```
安装后，执行uname -r，显示4.14.129-bbrplus则切换内核成功  
执行lsmod | grep bbr，显示有bbrplus则开启成功   

## 手动安装方法：  
1.  卸载本机的锐速（如果有）  

2.  下载内核  
wget --no-check-certificate https://github.com/Yuk1n0/Shadowsocks-Install/raw/master/Centos7/x86_64/kernel-4.14.129-bbrplus.rpm

3.  安装内核  
yum install -y kernel-4.14.129-bbrplus.rpm  

4.  切换启动内核  
grub2-set-default 'CentOS Linux (4.14.129-bbrplus) 7 (Core)'  

5.  设置fq  
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf  
设置bbrplus  
echo "net.ipv4.tcp_congestion_control=bbrplus" >> /etc/sysctl.conf  

6.  重启  
reboot  

7.  检查内核版本  uname -r  
显示4.14.129-bbrplus则成功  

8.  检查bbrplus是否已经启动  
lsmod | grep bbrplus  显示有tcp_bbrplus则成功  

## 卸载方法：  
安装别的内核bbrplus自动失效，卸载内核自行谷歌即可  

## 内核编译：  

只能用于4.14.x内核，更高版本的tcp部分源码有改动，要移植到高版本内核得自己研究  

下载4.14内核源码   
wget https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.14.91.tar.xz   

解压  
tar  -Jxvf  linux-4.14.91.tar.xz -C  /root/  

修改linux-4.14.91/include/net/inet_connection_sock.h，139行  
u64     icsk_ca_priv[112 / sizeof(u64)];  
#define ICSK_CA_PRIV_SIZE      (14 * sizeof(u64))  
这两段数值改为112和14，如上  

修改/net/ipv4/tcp_output.c#L，1823行  
tcp_snd_wnd_test函数大括号后}  
换行添加EXPORT_SYMBOL(tcp_snd_wnd_test);  

添加tcp_bbrplus.c，删除/net/ipv4/tcp_bbr.c  
修改linux-4.14.91/net/ipv4/Makefile，  
obj-$(CONFIG_TCP_CONG_BBR) += tcp_bbrplus.o，bbr改为bbrplus  

安装依赖  
**Centos**  
yum -y groupinstall Development tools  
yum -y install ncurses-devel bc gcc gcc-c++ ncurses ncurses-devel cmake elfutils-libelf-devel openssl-devel rpm-build redhat-rpm-config asciidoc hmaccalc perl-ExtUtils-Embed xmlto audit-libs-devel binutils-devel elfutils-devel elfutils-libelf-devel newt-devel python-devel zlib-devel  

**Debian**  
wget -qO- git.io/superupdate.sh | bash  
apt-get install build-essential libncurses5-dev  
apt-get build-dep linux  

切换到目录  
cd /root/linux-4.14.91  

配置  
make oldconfig  
或者  
make menuconfig  

确保CONFIG_TCP_CONG_BBR=m  

禁用签名调试  
scripts/config --disable MODULE_SIG  
scripts/config --disable DEBUG_INFO  

开始编译  
centos：make rpm-pkg  
debian：make deb-pkg
