#!/bin/bash
mkdir Shadowsocks
cd Shadowsocks

yum install -y gcc automake autoconf libtool make build-essential autoconf libtool
yum install -y curl curl-devel unzip zlib-devel openssl-devel perl perl-devel cpio expat-devel gettext-devel asciidoc xmlto nano

git clone https://github.com/FreeLinuxUser/Shadowsocks-libev.git
cd Shadowsocks-libev/
unzip master.zip

cd shadowsocks-libev*
./autogen.sh
./configure --prefix=/usr && make
make install

mkdir -p /etc/shadowsocks-libev
cp ./rpm/SOURCES/etc/init.d/shadowsocks-libev /etc/init.d/shadowsocks-libev
cp ./debian/config.json /etc/shadowsocks-libev/config.json
chmod +x /etc/init.d/shadowsocks-libev

nano /etc/shadowsocks-libev/config.json

service shadowsocks-libev start

chkconfig --add shadowsocks-libev
chkconfig shadowsocks-libev on
