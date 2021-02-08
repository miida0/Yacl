# Yacl

“如切如磋，如琢如磨。”

### 关于

另一份渗透测试及应急响应相关的Checklist。

------

### 信息收集

#### 出入口

- 外网出口
- C端
- WIFI
  - SSID
  - 认证信息
- VPN
  - 厂商
  - 登录方式
- 邮件网关
- App
- 小程序
  - 后台
  - 接口
- SSO
- 边界网络设备
- 运营商

#### 域名

- Whois
  - 搜索引擎
    - `site:domain`
  - [DNSDumpster](https://dnsdumpster.com/)
  - [Virustotal](https://www.virustotal.com/)
    - [api](https://developers.virustotal.com/v3.0/reference)
  - [CrtSearch](https://crt.sh/?)
  - [threatminer](https://www.threatminer.org/)
    - [api](https://www.threatminer.org/api.php)
  - [Censys](https://censys.io/ipv4)
    - [api](https://censys.io/product/product-data/)
- ASNx
  - `whois -h whois.radb.net -- '-i origin AS111111' | grep -Eo "([0-9.]+){4}/[0-9]+" | uniq`
  - `nmap --script targets-asn --script-args targets-asn.asn=15169`
- 域名相关
  - 查询域名注册邮箱
  - 通过域名查询备案号
  - 通过备案号查询域名
  - 反查注册邮箱
  - 反查注册人
  - 通过注册人查询到的域名再查询邮箱
  - 通过上一步邮箱去查询域名
  - 查询以上获取出的域名的子域名
- 域传送漏洞
- PassiveDNS
  - Virustotal
  - passivetotal
  - CIRCL
- 泛解析
  - 在子域名枚举时需要处理这种情况以防生成大量无效的记录
- 解析记录
  - CNAME
  - MX
    - Mail Exchanger
    - 用来寻找SMTP服务器信息
  - NS
    - Name Server
    - 查询指定域名由哪个DNS服务器来进行解析
  - SPF
    - Sender Policy Framework
    - 登记某个域名拥有的用来外发邮件的所有IP地址
    - 通过SPF记录可以获取相关的IP信息
- CDN
  - 验证
    - http://ping.chinaz.com/
    - https://asm.ca.com/en/ping.php
  - 子域名验证真实IP
    - 使用了CDN的域名的父域或者子域名不一定使用了CDN
  - 历史记录
    - 通过查找域名解析记录的方式去查找真实IP
  - 邮件
    - 社工收发邮件查看邮件头信息
  - 子域名爆破
    - 检测新域名上线
  - DNS Cache Snooping
    - 向DNS服务器发送域名解析请求可以探测是否使用了安全软件

#### 端口

- 21/TCP - FTP
  - 默认用户名密码 `anonymous:anonymous`
  - 爆破
  - Vsftpd版本后门
    - Vsftpd 2.3.4
- 22/TCP - SSH
  - 部分版本SSH存在漏洞可枚举用户名
  - 爆破
- 23/TCP - Telnet
  - 爆破
  - 嗅探抓明文密码
- 25/TCP - SMTP
  - 无认证时可伪造发件人
- 53/UDP - DNS
  - 域传送漏洞
  - DNS劫持
  - DNS缓存投毒
  - DNS欺骗
  - SPF
  - DDOS
    - DNS Query Flood
    - DNS反弹
  - DNS隧道
- 67/68 - DHCP
  - 劫持欺骗
- 69/TCP - TFTP
- 80/TCP - HTTP
- 88/TCP - Kerberos 
  - 监听KDC的票据请求
  - 黄金票据和白银票据的伪造
- 110/TCP - POP3
  - 爆破
- 135/TCP - RPC
  - wmic服务利用
- 137&138/ UDP - NetBIOS
  - 未授权访问
  - 弱口令
- 139/TCP - NetBIOS/Samba
  - 未授权访问
  - 弱口令
- 161/TCP - SNMP
  - Public弱口令
- 389/TCP - LDAP
  - 域上的权限验证服务
  - 匿名访问
  - 注入
- 443/TCP - HTTPS
- 445/TCP - SMB
  - 永恒之蓝
  - `net use \\192.168.1.1 /user:xxx\username password`
- 512/TCP & 513/TCP & 514/TCP - Linux Rexec
  - 弱口令
- 873/TCP - Rsync
  - 未授权访问
- 1025/TCP - RPC
  - NFS匿名访问
- 1090/TCP & 1099/TCP - Java RMI

### 工具

#### [Metasploit Framework](https://github.com/miida0/Yacl/blob/main/Metasploit%20Framework.md)

