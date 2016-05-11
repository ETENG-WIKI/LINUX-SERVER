# couchdb1.6.1 安装

转载自开源中国ETENG-HDP team 文档 http://hdputilcouchdb.mydoc.io/


ceteos 6.2  64位安装couchdb过程

yum install lrzsz 

进入存放源配置的文件夹
cd /etc/yum.repos.d

###**1.添加yum源epel支持,选择其中的一个.**
Install EPEL Repository

Install EPEL yum repository in your system, if not have already installed using one of below links.

CentOS/RHEL 6, 32 Bit (i386): 
```
# rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
``` 
CentOS/RHEL 6, 64 Bit x86_64): 
```
# rpm -Uvh http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm 
```
CentOS/RHEL 5, 32 Bit (i386): 
```
# rpm -Uvh http://dl.fedoraproject.org/pub/epel/5/i386/epel-release-5-4.noarch.rpm 
```
CentOS/RHEL 5, 64 Bit (x86_64): 
```
# rpm -Uvh http://dl.fedoraproject.org/pub/epel/5/x86_64/epel-release-5-4.noarch.rpm
```
###**2.yum报错的解决方案**
今天给Centos通过rpm -Uvh装了个epel的扩展后，执行yum就开始报错：
Error: Cannot retrieve metalink for repository: epel. Please verify its path and try again
在网上查了查，解决办法是编辑/etc/yum.repos.d/epel.repo，把基础的恢复，镜像的地址注释掉
```
#baseurl
mirrorlist
```
改成
```
baseurl
#mirrorlist 
```
###**3.安装依赖**

```
sudo yum install autoconf                     --成功  
sudo yum install autoconf-archive             ------失败  
sudo yum install automake                     ---成功  
sudo yum install curl-devel             --成功  
sudo yum install erlang-asn1            --成功 14B版本  
sudo yum install erlang-erts           --成功  
sudo yum install erlang-eunit           --成功  
sudo yum install erlang-os_mon          --成功  
sudo yum install erlang-xmerl           --成功  
sudo yum install help2man               --成功
sudo yum install js-devel               --成功 1.7.0版本  
sudo yum install libicu-devel           --成功  
sudo yum install libtool                --成功  
sudo yum install perl-Test-Harness      --成功 
``` 
 
官网下载couchdb 1.6.1
http://www.apache.org/dyn/closer.cgi?path=/couchdb/source/1.6.1/apache-couchdb-1.6.1.tar.gz

###**4.上传**
apache-couchdb-1.6.1.tar.gz

###5.解压
```
tar -zxvf  apache-couchdb-1.6.1.tar.gz 
```
切换到couchdb的目录
```
cd apache-couchdb-1.6.1
```
###6.编译
```
./configure --with-js-lib=/usr/local/spidermonkey/lib --with-js-include=/usr/local/spidermonkey/includes  --with-erlang=/usr/lib64/erlang/usr/include
```
有提示You have configured Apache CouchDB, time to relax. 说明编译成功

###7.安装
```
make && sudo make install
```
有提示
You have installed Apache CouchDB, time to relax. 说明安装成功

###8.添加用户
```
adduser -r --home /usr/local/var/lib/couchdb -M --shell /bin/bash --comment "CouchDB Administrator" couchdb
```
###9.赋予权限
```
chown -R couchdb:couchdb /usr/local/etc/couchdb
chown -R couchdb:couchdb /usr/local/var/lib/couchdb
chown -R couchdb:couchdb /usr/local/var/log/couchdb
chown -R couchdb:couchdb /usr/local/var/run/couchdb
chmod 0770 /usr/local/etc/couchdb
chmod 0770 /usr/local/var/lib/couchdb
chmod 0770 /usr/local/var/log/couchdb
chmod 0770 /usr/local/var/run/couchdb
```
###10.修改配置
[root@npm_private ~]#vi /usr/local/etc/couchdb/local.ini
[httpd]
;port = 5984
;bind_address = 127.0.0.1
###11.启动
```
/usr/local/etc/rc.d/couchdb start
```
是否安装成功
http://127.0.0.1:5984/_utils/index.html
成功访问管理界面安装成功.

###安装参考文献
http://docs.couchdb.org/en/1.6.1/install/unix.html  官网  

http://tecadmin.net/how-to-install-apache-couchdb-on-centosrhel-56/ 

http://my.oschina.net/shanhe/blog/296078#OSC_h2_2

http://blog.163.com/java_hxy/blog/static/1659024232014920101954825/

###couchdb简介

http://my.oschina.net/u/811958/blog/368640   couchdb简介

http://my.oschina.net/u/811958/blog/368642    couchdb简介

http://my.oschina.net/u/811958/blog/368656    couchdb文档

http://my.oschina.net/u/811958/blog/368661    couchdb视图


###couchdb java 连接框架

http://ektorp.org/





yum install gcc
yum install gcc-c++