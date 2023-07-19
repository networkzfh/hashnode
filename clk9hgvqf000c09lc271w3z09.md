---
title: "网络建设与运维第一套"
datePublished: Wed Jul 19 2023 08:50:29 GMT+0000 (Coordinated Universal Time)
cuid: clk9hgvqf000c09lc271w3z09
slug: 572r57uc5bu66k65lio6lq57u056ys5lia5awx
tags: linux

---

1.系统安装

（1）通过 PC1 web 连接 Server2，给 Server2 安装rocky-arm64 CLI

系统（语言为英文）。

（2）配置 Server2 的IPv4 地址为 10.1.220.100/24。

（3） 安装 qemu 和virt-install。

（4） 创建 rocky-arm64 虚拟机，虚拟机硬盘文件保存在默认目录，名称为linuxN.qcow2(N 表示虚拟机编号 1-9，如虚拟机 linux1 的硬盘文件为linux1.qcow2,虚拟机linux2 的硬盘文件为linux2.qcow2), 虚拟机信息如下：

<table><tbody><tr><td colspan="1" rowspan="1"><p>虚拟机名称</p></td><td colspan="1" rowspan="1"><p>vcpu</p></td><td colspan="1" rowspan="1"><p>内存</p></td><td colspan="1" rowspan="1"><p>硬盘</p></td><td colspan="1" rowspan="1"><p>IPv4 地址</p></td><td colspan="1" rowspan="1"><p>完全合格域名</p></td></tr><tr><td colspan="1" rowspan="1"><p>linux1</p></td><td colspan="1" rowspan="1"><p>2</p></td><td colspan="1" rowspan="1"><p>4096MB</p></td><td colspan="1" rowspan="1"><p>40GB</p></td><td colspan="1" rowspan="1"><p>10.1.220.101/24</p></td><td colspan="1" rowspan="1"><p>linux1.skills.lan</p></td></tr><tr><td colspan="1" rowspan="1"><p>linux2</p></td><td colspan="1" rowspan="1"><p>2</p></td><td colspan="1" rowspan="1"><p>4096MB</p></td><td colspan="1" rowspan="1"><p>40GB</p></td><td colspan="1" rowspan="1"><p>10.1.220.102/24</p></td><td colspan="1" rowspan="1"><p>linux2.skills.lan</p></td></tr><tr><td colspan="1" rowspan="1"><p>linux3</p></td><td colspan="1" rowspan="1"><p>2</p></td><td colspan="1" rowspan="1"><p>4096MB</p></td><td colspan="1" rowspan="1"><p>40GB</p></td><td colspan="1" rowspan="1"><p>10.1.220.103/24</p></td><td colspan="1" rowspan="1"><p>linux3.skills.lan</p></td></tr><tr><td colspan="1" rowspan="1"><p>linux4</p></td><td colspan="1" rowspan="1"><p>2</p></td><td colspan="1" rowspan="1"><p>4096MB</p></td><td colspan="1" rowspan="1"><p>40GB</p></td><td colspan="1" rowspan="1"><p>10.1.220.104/24</p></td><td colspan="1" rowspan="1"><p>linux4.skills.lan</p></td></tr><tr><td colspan="1" rowspan="1"><p>linux5</p></td><td colspan="1" rowspan="1"><p>2</p></td><td colspan="1" rowspan="1"><p>4096MB</p></td><td colspan="1" rowspan="1"><p>40GB</p></td><td colspan="1" rowspan="1"><p>10.1.220.105/24</p></td><td colspan="1" rowspan="1"><p>linux5.skills.lan</p></td></tr><tr><td colspan="1" rowspan="1"><p>linux6</p></td><td colspan="1" rowspan="1"><p>2</p></td><td colspan="1" rowspan="1"><p>4096MB</p></td><td colspan="1" rowspan="1"><p>40GB</p></td><td colspan="1" rowspan="1"><p>10.1.220.106/24</p></td><td colspan="1" rowspan="1"><p>linux6.skills.lan</p></td></tr><tr><td colspan="1" rowspan="1"><p>linux7</p></td><td colspan="1" rowspan="1"><p>2</p></td><td colspan="1" rowspan="1"><p>4096MB</p></td><td colspan="1" rowspan="1"><p>40GB</p></td><td colspan="1" rowspan="1"><p>10.1.220.107/24</p></td><td colspan="1" rowspan="1"><p>linux7.skills.lan</p></td></tr><tr><td colspan="1" rowspan="1"><p>linux8</p></td><td colspan="1" rowspan="1"><p>2</p></td><td colspan="1" rowspan="1"><p>4096MB</p></td><td colspan="1" rowspan="1"><p>40GB</p></td><td colspan="1" rowspan="1"><p>10.1.220.108/24</p></td><td colspan="1" rowspan="1"><p>linux8.skills.lan</p></td></tr><tr><td colspan="1" rowspan="1"><p>linux9</p></td><td colspan="1" rowspan="1"><p>2</p></td><td colspan="1" rowspan="1"><p>4096MB</p></td><td colspan="1" rowspan="1"><p>40GB</p></td><td colspan="1" rowspan="1"><p>10.1.220.109/24</p></td><td colspan="1" rowspan="1"><p>linux9.skills.lan</p></td></tr></tbody></table>

（5） 安装 linux

（6） 1，系统为rocky-arm64 CLI，网卡、硬盘、显示驱动均为virtio，网络模式为桥接模式。

（ 6 ） 关闭 linux1 ，给 linux1 创建快照， 快照名称为

linux-snapshot。

（7）根据 linux1 克隆虚拟机linux2-linux9。2.dns 服务

任务描述：创建DNS 服务器，实现企业域名访问。

（1）       所有 linux 主机启用防火墙，防火墙区域为 public，在防火墙中放行对应服务端口。

firewall-cmd --get-default-zone

public

（2）       利用 chrony，配置 linux1 为其他linux 主机提供NTP 服务。

（3）       所有 linux 主机之间（包含本主机）root 用户实现密钥 ssh

认证，禁用密码认证。

（4）       利用 bind，配置 linux1 为主DNS 服务器，linux2 为备用DNS

服务器。为所有linux 主机提供冗余DNS 正反向解析服务。

（5）       配置 linux1 为 CA 服务器,为 linux 主机颁发证书。证书颁发机构有效期 10 年，公用名为 linux1.skills.lan。申请并颁发一张

供 linux 服务器使用的证书， 证书信息： 有效期=5 年， 公用名

\=skills.lan，国家=CN，省=Beijing，城市=Beijing，组织=skills， 组织单位=system，使用者可选名称=\*.skills.lan 和skills.lan。将证书 skills.crt 和私钥 skills.key 复制到需要证书的 linux 服务器

/etc/ssl 目录。浏览器访问https 网站时，不出现证书警告信息。

3\. ansible 服务

任务描述：请采用ansible，实现自动化运维。

（1）在 linux1 上安装 ansible，作为 ansible 的控制节点。

linux2-linux9 作为 ansible 的受控节点。

4\. apache2 服务

任务描述：请采用Apache 搭建企业网站。

（1）     ） 配置 linux1 为 Apache2 服务器，使用 skills.lan 或 any.skills.lan（any 代表任意网址前缀，用 linux1.skills.lan 和 web.skills.lan 测试）访问时，自动跳转到 [www.skills.lan](http://www.skills.lan/)。禁止使用 IP 地址访问，默认首页文档/var/www/html/index.html 的内容为 "apache"。

（2）     把/etc/ssl/skills.crt 证书文件和/etc/ssl/skills.key 私钥文件转换成含有证书和私钥的/etc/ssl/skills.pfx 文件；然后把

/etc/ssl/skills.pfx 转换为含有证书和私钥的/etc/ssl/skills.pem 文件，再从/etc/ssl/skills.pem 文件中提取证书和私钥分别到

/etc/ssl/apache.crt 和/etc/ssl/apache.key。

（3）     客户端访问 Apache 服务时，必需有 ssl 证书。

5\. tomcat 服务

任务描述：采用Tomcat 搭建动态网站。

（1）    配置linux2 为nginx 服务器，默认文档index.html 的内容

为“hellonginx”；仅允许使用域名访问，http 访问自动跳转到 https。

（2）    利用 nginx 反向代理，实现 linux3 和 linux4 的 tomcat 负载均衡，通过https://tomcat.skills.lan 加密访问Tomcat，http 访问通过 301 自动跳转到 https。

（3）    配置 linux3 和 linux4 为 tomcat 服务器，网站默认首页内容分别为“tomcatA”和“tomcatB”，仅使用域名访问 80 端口http 和 443 端口https；证书路径均为/etc/ssl/skills.jks。

6\. samba 服务

任务描述：请采用samba 服务，实现资源共享。

（1） 在 linux3 上创建 user00-user19 等 20 个用户；user00 和user01 添加到 manager 组，user02 和 user03 添加到 dev 组。把用户user00-user03 添加到samba 用户。

（2） 配置 linux3 为samba 服务器,建立共享目录/srv/sharesmb，共享名与目录名相同。manager 组用户对 sharesmb 共享有读写权限， dev 组对 sharesmb 共享有只读权限；用户对自己新建的文件有完全权限，对其他用户的文件只有读权限，且不能删除别人的文件。在本机用smbclient 命令测试。

（3） 在 linux4 修改/etc/fstab,使用用户 user00 实现自动挂载

linux3 的sharesmb 共享到/sharesmb。

7\. nfs 服务

任务描述：请采用nfs，实现共享资源的安全访问。

（1）    配置 linux2 为kdc 服务器，负责 linux3 和linux4 的验证。

（2）    在 linux3 上，创建用户，用户名为xiao，uid=222，gid=222，家目录为/home/xiaodir。

（3）    配置 linux3 为nfs 服务器，目录/srv/sharenfs 的共享要求

为：linux 服务器所在网络用户有读写权限，所有用户映射为 xiao， kdc 加密方式为krb5p。

（4）    配置 linux4 为 nfs 客户端，利用 autofs 按需挂载 linux3 上的/srv/sharenfs 到/sharenfs 目录，挂载成功后在该目录创建 test 目录。

8\. kubernetes 服务

任务描述：请采用kubernetes 和containerd，管理容器。

（1）     在 linux5-linux7 上安装 containerd 和kubernetes，linux6作为 master node ， linux6 和 linux7 作为 work node ； 使用 containerd.sock 作为容器 runtime-endpoint。导入 nginx 镜像，主页内容为“HelloKubernetes”。

（2）     master 节点配置calico，作为网络组件。

（3）     创建一个 deployment，名称为 web，副本数为 2；创建一个服务，类型为nodeport，名称为web，映射本机 80 端口和 443 端口分别到容器的 80 端口和 443 端口。

9\. ftp 服务

任务描述：请采用FTP 服务器，实现文件安全传输。

（1）     配置linux2 为FTP 服务器，安装vsftpd，新建本地用户test，本地用户登陆 ftp 后的目录为/var/ftp/pub，可以上传下载。

（2）     配置ftp 虚拟用户认证模式，虚拟用户 ftp1 和ftp2 映射 为 ftp，ftp1 登录 ftp 后的目录为/var/ftp/vdir/ftp1，可以上传下载,禁止上传后缀名为.docx 的文件； ftp2 登录 ftp 后的目录为

/var/ftp/vdir/ftp2，仅有下载权限。

（3）     使用 ftp 命令在本机验证。

10\. iscsi 服务

任务描述：请采用iscsi，搭建存储服务。

（1）    为 linux8 添加 4 块硬盘，每块硬盘大小为 5G，创建 lvm 卷，卷组名为 vg1，逻辑卷名为 lv1，容量为全部空间，格式化为 ext4 格式。使用/dev/vg1/lv1 配置为iSCSI 目标服务器，为 linux9 提供iSCSI服务。iSCSI 目标端的 wwn 为iqn.2023-08.lan.skills:server, iSCSI发起端的wwn 为iqn.2023-08.lan.skills:client。

（2）    配置linux9 为iSCSI 客户端，实现discovery chap 和session chap 双向认证， Target 认证用户名为 IncomingUser ， 密码为 IncomingPass ； Initiator 认证用户名为OutgoingUser ， 密码为 OutgoingPass。修改/etc/rc.d/rc.local 文件开机自动挂载 iscsi 硬盘到/iscsi 目录。

11\. mysql 服务

任务描述：请安装mysql 服务，建立数据表。

（1） 配置 linux2 为 mysql 服务器，创建数据库用户 xiao，在任意机器上对所有数据库有完全权限。

（2） 创建数据库 userdb；在库中创建表 userinfo，表结构如下：

<table><tbody><tr><td colspan="1" rowspan="1"><p>字段名</p></td><td colspan="1" rowspan="1"><p>数据类型</p></td><td colspan="1" rowspan="1"><p>主键</p></td><td colspan="1" rowspan="1"><p>自增</p></td></tr><tr><td colspan="1" rowspan="1"><p>id</p></td><td colspan="1" rowspan="1"><p>int</p></td><td colspan="1" rowspan="1"><p>是</p></td><td colspan="1" rowspan="1"><p>是</p></td></tr><tr><td colspan="1" rowspan="1"><p>name</p></td><td colspan="1" rowspan="1"><p>varchar(10)</p></td><td colspan="1" rowspan="1"><p>否</p></td><td colspan="1" rowspan="1"><p>否</p></td></tr><tr><td colspan="1" rowspan="1"><p>birthday</p></td><td colspan="1" rowspan="1"><p>datetime</p></td><td colspan="1" rowspan="1"><p>否</p></td><td colspan="1" rowspan="1"><p>否</p></td></tr><tr><td colspan="1" rowspan="1"><p>sex</p></td><td colspan="1" rowspan="1"><p>varchar(5)</p></td><td colspan="1" rowspan="1"><p>否</p></td><td colspan="1" rowspan="1"><p>否</p></td></tr><tr><td colspan="1" rowspan="1"><p>password</p></td><td colspan="1" rowspan="1"><p>varchar(200)</p></td><td colspan="1" rowspan="1"><p>否</p></td><td colspan="1" rowspan="1"><p>否</p></td></tr></tbody></table>

（3）在表中插入 2 条记录，分别为(1,user1，1999-07-01，男)， (2,user2，1999-07-02，女)，password 与name 相同，password 字段用password 函数加密。

（4）     ） 修改表 userinfo 的结构， 在 name 字段后添加新字段

height(数据类型为 float)，更新 user1 和 user2 的 height 字段内容

为 1.61 和 1.62。

（5）     新建/var/mysqlbak/userinfo.txt 文件，文件内容如下， 然后将文件内容导入到 userinfo 表中，password 字段用 password 函数加密。

3,user3,1.63,1999-07-03,女,user3

4,user4,1.64,1999-07-04,男,user4

5,user5,1.65,1999-07-05,男,user5

6,user6,1.66,1999-07-06,女,user6

7,user7,1.67,1999-07-07,女,user7

8,user8,1.68,1999-07-08,男,user8

9,user9,1.69,1999-07-09,女,user9

（6）     将表 userinfo 的记录导出，存放到/var/databak/mysql.sql，字段之间用','分隔。

（7）     每周五凌晨 1:00 以 root 用户身份备份数据库 userdb 到

/var/databak/userdb.sql(含创建数据库命令)。12.docker 服务

任务描述：请采用podman，实现有守护程序的容器应用。

（1） 在linux2 上安装docker-ce，导入rocky 镜像。

（2） 创建名称为skills 的容器，映射本机的 8000 端口到容器的

80 端口，在容器内安装 apache2，默认网页内容为“HelloDocker”。

（3） 配置 docker 私有仓库。

[13.shell](http://13.shell) 脚本

任务描述：请采用shell 脚本,实现快速批量的操作。

（1）在 linux4 上编写/root/createfile.sh 的shell 脚本，创建20 个文件/root/shell/file00 至/root/shell/file19，如果文件存在，则删除再创建；每个文件的内容同文件名，如 file00 文件的内容为\[“file00”。用/root/createfile.sh命令测试。

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689755612521/cd5d06f4-b8fa-4fdb-ae8f-a1bc4f27edba.jpeg align="center")

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">加油</div>
</div>

---

<iframe src="//player.bilibili.com/player.html?aid=763585659&amp;bvid=BV1yr4y127od&amp;cid=423837922&amp;page=1"> </iframe>