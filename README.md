# NPS 内网穿透 (全修)

[![GitHub Stars](https://img.shields.io/github/stars/djylb/nps.svg)](https://github.com/djylb/nps)
[![GitHub Forks](https://img.shields.io/github/forks/djylb/nps.svg)](https://github.com/djylb/nps)
[![Release](https://github.com/djylb/nps/workflows/Release/badge.svg)](https://github.com/djylb/nps/actions)
[![GitHub All Releases](https://img.shields.io/github/downloads/djylb/nps/total)](https://github.com/djylb/nps/releases)

> 由于 GitHub 限制浏览器语言为中文（Accept-Language=zh-CN) 访问 *.githubusercontent.com ，图标可能无法正常显示。

- [English](https://github.com/djylb/nps/blob/master/README_en.md)

---

## 简介

NPS 是一款轻量高效的内网穿透代理服务器，支持多种协议（TCP、UDP、HTTP、HTTPS、SOCKS5 等）转发。它提供直观的 Web 管理界面，使得内网资源能安全、便捷地在外网访问，同时满足多种复杂场景的需求。

由于[NPS](https://github.com/ehang-io/nps)停更已久，本仓库基于 nps 0.26 整合社区更新二次开发而来。

- **提问前请先查阅：**  [文档](https://d-jy.net/docs/nps/) 与 [Issues](https://github.com/djylb/nps/issues)
- **欢迎参与：**  提交 PR、反馈问题或建议，共同推动项目发展。
- **讨论交流：**  加入 [Telegram 交流群](https://t.me/npsdev) 与其他用户交流经验。
- **Android：**  [djylb/npsclient](https://github.com/djylb/npsclient)
- **OpenWrt：**  [djylb/nps-openwrt](https://github.com/djylb/nps-openwrt)

---

## 主要特性

- **多协议支持**  
  TCP/UDP 转发、HTTP/HTTPS 转发、HTTP/SOCKS5 代理、P2P 模式、Proxy Protocol支持等，满足各种内网访问场景。

- **跨平台部署**  
  支持 Linux、Windows 等主流平台，可轻松安装为系统服务。

- **Web 管理界面**  
  实时监控流量、连接情况以及客户端状态，操作简单直观。

- **安全与扩展**  
  内置加密传输、流量限制、到期限制、证书管理等多重功能，保障数据安全。

---

## 安装与使用

更多详细配置请参考 [文档](https://d-jy.net/docs/nps/)（部分内容可能未更新）。

### [Android](https://github.com/djylb/npsclient) | [OpenWrt](https://github.com/djylb/nps-openwrt)

### Docker 部署

***DockerHub***： [NPS](https://hub.docker.com/r/duan2001/nps) [NPC](https://hub.docker.com/r/duan2001/npc)

***GHCR***： [NPS](https://github.com/djylb/nps/pkgs/container/nps) [NPC](https://github.com/djylb/nps/pkgs/container/npc)

> 有真实IP获取需求可配合 [mmproxy](https://github.com/djylb/mmproxy-docker) 使用。例如：SSH

#### NPS 服务端
```bash
docker pull duan2001/nps
docker run -d --restart=always --name nps --net=host -v $(pwd)/conf:/conf -v /etc/localtime:/etc/localtime:ro duan2001/nps
```

#### NPC 客户端
```bash
docker pull duan2001/npc
docker run -d --restart=always --name npc --net=host duan2001/npc -server=xxx:123,yyy:456 -vkey=key1,key2 -type=tls,tcp -log=off
```

### 服务端安装

#### Linux
```bash
# 安装（默认配置路径：/etc/nps/；二进制文件路径：/usr/bin/）
./nps install
nps start|stop|restart|uninstall

# 更新
nps stop
nps-update update
nps start
```

#### Windows
> Windows 7 用户请使用 old 结尾版本 [64](https://github.com/djylb/nps/releases/latest/download/windows_amd64_server_old.tar.gz) / [32](https://github.com/djylb/nps/releases/latest/download/windows_386_server_old.tar.gz) （需要手动更新）
```powershell
.\nps.exe install
.\nps.exe start|stop|restart|uninstall

# 更新
.\nps.exe stop
.\nps-update.exe update
.\nps.exe start
```

### 客户端安装

#### Linux
```bash
./npc install
/usr/bin/npc install -server=xxx:123,yyy:456 -vkey=xxx,yyy -type=tls -log=off
npc start|stop|restart|uninstall

# 更新
npc stop
/usr/bin/npc-update update
npc start
```

#### Windows
> Windows 7 用户请使用 old 结尾版本 [64](https://github.com/djylb/nps/releases/latest/download/windows_amd64_client_old.tar.gz) / [32](https://github.com/djylb/nps/releases/latest/download/windows_386_client_old.tar.gz) （需要手动更新）
```powershell
.\npc.exe install -server="xxx:123,yyy:456" -vkey="xxx,yyy" -type="tls,tcp" -log="off"
.\npc.exe start|stop|restart|uninstall

# 更新
.\npc.exe stop
.\npc-update.exe update
.\npc.exe start
```

> **提示：** 客户端支持同时连接多个服务器，示例：  
> `npc -server=xxx:123,yyy:456,zzz:789 -vkey=key1,key2,key3 -type=tcp,tls`  
> 这里 `xxx:123` 使用 tcp, `yyy:456` 和 `zzz:789` 使用tls

---

## 更新日志

### DEV

- **Main** 
  - 待定，优先修BUG，新功能随缘更新

### Stable

- **v0.26.55 (2025-05-05)**
  - 文档添加自动翻译
  - 重写日志输出模块
  - 修复日志轮换功能
  - 修复日志权限问题 [#70](https://github.com/djylb/nps/issues/70)
  - 更新上游依赖

- **v0.26.54 (2025-05-02)**
  - 更新文档说明
  - 添加弹窗翻译
  - 优化浏览器语言检测
  - 优化操作逻辑减少操作步骤 [#69](https://github.com/djylb/nps/issues/69)

- **v0.26.53 (2025-04-25)**
  - P2P同时转发TCP和UDP端口

- **v0.26.52 (2025-04-23)**
  - 优化服务器域名解析逻辑
  - 修复同时启用TCP和KCP时客户端不同步问题

- **v0.26.51 (2025-04-22)**
  - 优化P2P打洞算法
  - 使用迭代法解析服务器域名
  - 优选最快IP连接服务器
  - 允许同时监听KCP端口

- **v0.26.50 (2025-04-19)**
  - 优化P2P探测和连接速度
  - 隧道编辑页面支持保存为新配置 [#8](https://github.com/djylb/nps/issues/8)
  - 调整页面显示，添加排序支持

- **v0.26.49 (2025-04-18)**
  - vkey添加点击复制
  - 重写透明代理逻辑 [#59](https://github.com/djylb/nps/issues/59)
  - 修复linux、darwin、freebsd的透明代理

- **v0.26.48 (2025-04-17)**
  - 添加点击自动复制命令行 [#62](https://github.com/djylb/nps/issues/62)
  - 密码认证配置内容忽略空行
  - 修复NPS的IPv6自动识别
  - 修复管理页面显示
  - 隧道列表支持端口号排序
  - 重写客户端TLS功能，支持使用type传入tls （已弃用tls_enable）
  - 重写服务端TLS功能，支持TLS端口复用 （已弃用tls_enable）
  - 客户端支持连接多个服务器 [#9](https://github.com/djylb/nps/issues/9)
  - 更新证书随机生成

- **v0.26.47 (2025-04-14)** 
  - 优化P2P处理逻辑
  - 服务端支持配置`p2p_ip=0.0.0.0`来自动识别IP地址(IPv4/IPv6由`dns_server`配置决定)
  - 服务端支持配置`p2p_ip=::`来强制自动识别使用IPv6地址
  - 修复P2P的IPv6支持
  - NPC自动选择IPv4/IPv6进行P2P连接
  - **新增** 支持单条隧道独立配置密码认证

- **v0.26.46 (2025-04-14)** 
  - 调整日志输出等级
  - 优化写入性能
  - 修复端口复用时连接泄露和并发冲突
  - 清理代码更新相关依赖
  - 新增OpenWRT仓库 [djylb/nps-openwrt](https://github.com/djylb/nps-openwrt)
  - 修复拼写错误
  - 自动更新[Android](https://github.com/djylb/npsclient)和[OpenWrt](https://github.com/djylb/nps-openwrt)仓库
  - 自动识别服务器IP [#59](https://github.com/djylb/nps/issues/59)
  - P2P支持IPv6（需要纯IPv6网络环境）

- **v0.26.45 (2025-04-09)** 
  - 搜索功能匹配不限制大小写
  - 修复HTTP代理认证头 [#55](https://github.com/djylb/nps/issues/55)
  - 添加编译架构 [#53](https://github.com/djylb/nps/issues/53)
  - 增加自定义DNS支持非标准系统
  - 新增安卓客户端 [#53](https://github.com/djylb/nps/issues/53) [djylb/npsclient](https://github.com/djylb/npsclient)
  - 美化下拉框样式，使用标准JSON保存数据 [#51](https://github.com/djylb/nps/pull/51) (感谢[yhl452493373](https://github.com/yhl452493373))

- **v0.26.44 (2025-03-26)** 
  - 修复客户端超过1000不显示问题
  - **增强** 隧道添加支持搜索客户端

- **v0.26.43 (2025-03-24)** 
  - 修复客户端隧道编辑按钮缺失
  - 隧道列表隐藏无用信息
  - **新增** 域名转发隧道支持暂停
  - **增强** 域名转发防止扫描探测

- **v0.26.42 (2025-03-23)** 
  - 修复管理页面表单Id标签重复
  - 修复隧道页面不显示
  - 整理nps.conf文件

- **v0.26.41 (2025-03-22)** 
  - Docker自动创建NPS默认配置 **（一定要记得改配置）**
  - 固定管理页面左侧菜单、顶部标题、底部footer [#49](https://github.com/djylb/nps/pull/49)
  - 优化运行速度，减少资源占用
  - 修复单条隧道流量统计 [#30](https://github.com/djylb/nps/issues/30)
  - 增强流量统计颗粒度 **（注意：客户端流量是隧道流量出入总和的两倍）**
  - 修复文件模式访问
  - 调整管理页面文件模式显示
  - **新增** 管理页面表单选项持久化储存
  - **新增** 表单添加显示全部选项
  - **新增** 单条隧道支持限制流量和时间
  - 调整隧道页面显示
  - 修复NPC客户端NAT检测  

- **v0.26.40 (2025-03-21)** 
  - 前端页面美化 [#47](https://github.com/djylb/nps/pull/47)
  - 增加docker支持架构，添加shell支持
  - 向NPS的docker镜像添加tzdata软件包支持时区配置 [#45](https://github.com/djylb/nps/issues/45)
  - 私密代理支持通过TLS连接 [#37](https://github.com/djylb/nps/issues/37)
  - docker添加主线分支发布
  - 修复连接数统计问题 [#48](https://github.com/djylb/nps/issues/48)

- **v0.26.39 (2025-03-16)** 
  - 切换包至本仓库
  - 更新说明文档至当前版本
  - 更新管理页面帮助
  - 优化 nps.conf 配置文件
  - 更新 SDK 组件

- **v0.26.38 (2025-03-14)** 
  - 域名转发支持HTTP/2
  - 当配置请求域名修时同时修改Origin头避免后端监测
  - 调整域名编辑页面逻辑
  - 更新相关依赖，修复CVE-2025-22870
  - 使用 [XTLS/go-win7](https://github.com/XTLS/go-win7) 编译旧版代码支持Win7
  - 整理仓库代码
  - 优化域名查找算法

更多历史更新记录请参阅项目 [Releases](https://github.com/djylb/nps/releases)

一、使用linux服务器进行搭建nps
nps项目地址：https://github.com/ehang-io/nps/releases

首先下载linux server端

wget https://github.com/ehang-io/nps/releases/download/v0.26.10/linux_amd64_server.tar.gz

如果服务器下载失败，则可以进入项目地址单独下载  linux_amd64_server.tar.gz

使用  tar -zxvf linux_amd64_server.tar.gz  指令进行解压

使用  ./nps install  进行安装nps

完成之后编辑  /etc/nps/conf/nps.conf

#web下面是web界面的相关设定

web_username=用户名称

web_password=用户密码

web_port =web界面的端口号

#HTTP(S) proxy port, no startup if empty

http_proxy_port=80 端口号随意，不占用所需端口即可

https_proxy_port=443  端口号随意，不占用所需端口即可

##bridge下面是客户端连接服务端的设置，端口号可自定，其他可不动

bridge_type=tcp

bridge_port=8024

bridge_ip=0.0.0.0

为安全性（nps有这个漏洞）考虑的话，去掉

#auth_key=test

前面的#号并且将test改成乱码，比如

auth_key=etsysudusa

并将

auth_crypt_key=1234567812345678

也改为乱码，比如

auth_crypt_key=rghusiohfnaibfbuegois

然后输入  nps restart  进行重启nps

服务器如果是端口映射则需要映射web端口和客户端连接端口

使用公网地址进入web页面登录

选择客户端，点击新增，可自由选择，也可啥也不动

新增之后刷新，点击刚刚创建的客户端的加号

里面的连接指令就是在客户端需要执行的

二、使用linux连接nps
首先下载linux client端

wget https://github.com/ehang-io/nps/releases/download/v0.26.10/linux_amd64_client.tar.gz

如果服务器下载失败，则可以进入项目地址单独下载  linux_amd64_client.tar.gz

使用  tar -zxvf linux_amd64_client.tar.gz  指令进行解压

然后直接输入连接指令即可连接（如果nps所在服务器是端口映射的，请将连接指令中的网址改为映射出去的外网地址）

如果想让该映射自启动且不占用ssh，可在指令中添加  install  比如:

./npc install -server=127.0.0.1:8024 -vkey=8eursdtstsqwrssts04x -type=tcp

然后输入npc start进行启动，这时候npc服务可跟随系统自动启动以及后台运行。

进入nps的web端的客户端页可看到是否连接成功

若显示在线，点击隧道，然后进行端口映射

点击新增，服务器端口就是映射出去后的端口，目标端口为需要映射的端口

协议一般tcp即可

三、使用windows服务器进行搭建nps
首先下载windows server端

https://github.com/ehang-io/nps/releases/download/v0.26.10/windows_386_server.tar.gz

解压，配置文件在conf/nps.conf中，参考linux server搭建进行编辑

运行nps.exe

web操作同linux

四、使用windows服务器进行连接nps
首先下载windows client端

https://github.com/ehang-io/nps/releases/download/v0.26.10/windows_amd64_client.tar.gz

解压，在该目录打开cmd窗口，输入连接指令,删除./,比如

npc -server=127.0.0.1:8024 -vkey=ysyststststs4x -type=tcp

web操作同linux

基本使用
无配置文件模式
此模式的各种配置在服务端web管理中完成,客户端除运行一条命令外无需任何其他设置

 ./npc -server=ip:port -vkey=web界面中显示的密钥

注册到系统服务(开机启动、守护进程)
对于linux、darwin

注册：sudo ./npc install 其他参数（例如-server=xx -vkey=xx或者-config=xxx）

启动：sudo npc start

停止：sudo npc stop

如果需要更换命令内容需要先卸载./npc uninstall，再重新注册
对于windows，使用管理员身份运行cmd

注册：npc.exe install 其他参数（例如-server=xx -vkey=xx或者-config=xxx）

启动：npc.exe start

停止：npc.exe stop

如果需要更换命令内容需要先卸载npc.exe uninstall，再重新注册
如果需要当客户端退出时自动重启客户端，请按照如图所示配置 image
注册到服务后，日志文件windows位于当前目录下，linux和darwin位于/var/log/npc.log

客户端更新
首先进入到对于的客户端二进制文件目录

请首先执行sudo npc stop或者npc.exe stop停止运行，然后

对于linux

 sudo npc-update update

对于windows

npc-update.exe update

更新完成后，执行执行sudo npc start或者npc.exe start重新运行即可完成升级

如果无法更新成功，可以直接自行下载releases压缩包然后覆盖原有的npc二进制文件

配置文件模式
此模式使用nps的公钥或者客户端私钥验证，各种配置在客户端完成，同时服务端web也可以进行管理

 ./npc -config=npc配置文件路径
配置文件说明
示例配置文件

全局配置

[common]
server_addr=1.1.1.1:8024
conn_type=tcp
vkey=123
username=111
password=222
compress=true
crypt=true
rate_limit=10000
flow_limit=100
remark=test
max_conn=10
#pprof_addr=0.0.0.0:9999

项	含义
server_addr	服务端ip/域名:port
conn_type	与服务端通信模式(tcp或kcp)
vkey	服务端配置文件中的密钥(非web)
username	socks5或http(s)密码保护用户名(可忽略)
password	socks5或http(s)密码保护密码(可忽略)
compress	是否压缩传输(true或false或忽略)
crypt	是否加密传输(true或false或忽略)
rate_limit	速度限制，可忽略
flow_limit	流量限制，可忽略
remark	客户端备注，可忽略
max_conn	最大连接数，可忽略
pprof_addr	debug pprof ip:port

域名代理

[common]
server_addr=1.1.1.1:8024
vkey=123
[web1]
host=a.proxy.com
target_addr=127.0.0.1:8080,127.0.0.1:8082
host_change=www.proxy.com
header_set_proxy=nps

项	含义

web1	备注
host	域名(http
target_addr	内网目标，负载均衡时多个目标，逗号隔开
host_change	请求host修改
header_xxx	请求header修改或添加，header_proxy表示添加header proxy:nps

tcp隧道模式

[common]
server_addr=1.1.1.1:8024
vkey=123
[tcp]
mode=tcp
target_addr=127.0.0.1:8080
server_port=9001

项	含义

mode	tcp
server_port	在服务端的代理端口
tartget_addr	内网目标

udp隧道模式

[common]
server_addr=1.1.1.1:8024
vkey=123
[udp]
mode=udp
target_addr=127.0.0.1:8080
server_port=9002

项	含义

mode	udp
server_port	在服务端的代理端口
target_addr	内网目标

http代理模式

[common]
server_addr=1.1.1.1:8024
vkey=123
[http]
mode=httpProxy
server_port=9003

项	含义

mode	httpProxy
server_port	在服务端的代理端口

socks5代理模式

[common]
server_addr=1.1.1.1:8024
vkey=123
[socks5]
mode=socks5
server_port=9004
multi_account=multi_account.conf

项	含义

mode	socks5
server_port	在服务端的代理端口
multi_account	socks5多账号配置文件（可选),配置后使用basic_username和basic_password无法通过认证

私密代理模式

[common]
server_addr=1.1.1.1:8024
vkey=123
[secret_ssh]
mode=secret
password=ssh2
target_addr=10.1.50.2:22

项	含义

mode	secret
password	唯一密钥
target_addr	内网目标

p2p代理模式

[common]
server_addr=1.1.1.1:8024
vkey=123
[p2p_ssh]
mode=p2p
password=ssh2
target_addr=10.1.50.2:22

项	含义

mode	p2p
password	唯一密钥
target_addr	内网目标

文件访问模式

利用nps提供一个公网可访问的本地文件服务，此模式仅客户端使用配置文件模式方可启动

[common]
server_addr=1.1.1.1:8024
vkey=123
[file]
mode=file
server_port=9100
local_path=/tmp/
strip_pre=/web/

项	含义

mode	file
server_port	服务端开启的端口
local_path	本地文件目录
strip_pre	前缀
对于strip_pre，访问公网ip:9100/web/相当于访问/tmp/目录

断线重连
[common]
auto_reconnection=true
