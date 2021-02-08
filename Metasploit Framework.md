# Metasploit Framework

### 参考

- [Metasploit Framework Handbook](https://www.anquanke.com/post/id/209966#)

### 结构

#### auxiliary - 辅助模块

- 扫描查点
- 虚假服务
- 收集密码
- 口令爆破
- 信息嗅探
- 信息泄露
- Fuzz测试
- 协议欺骗

#### exploits - 渗透攻击模块

- 主动渗透攻击
  - 通过目标端口
- 被动渗透攻击
  - 目标客户端软件漏洞
  - 欺骗钓鱼

#### payloads - 攻击荷载模块

- 独立(Singles)
  - 自包含
- 传输器(Stager)
  - `windwos/shell/bind_tcp`中`bind_tcp`是`Stager`
- 传输体(Stage)
  - `windwos/shell/bind_tcp`中`shell`是`Stage`

#### nops - 空指令模块

- 增加`Shellcoede`的安全着陆区防止执行失败

#### encoders - 编码器模块

- 避免出现脏数据
- 对`Payloads`进行免杀处理

#### post - 后渗透攻击模块

- 敏感信息
- 跳板攻击
- `Meterpreter`
  - 本地攻击
  - 内网拓展

#### evasion - 免杀模块

- 被**encoders**模块调用实现免杀

### 功能阶段

#### 情报搜集

- 目标识别、服务枚举
- 内建扫描器
- 集成Nmap、Nessus、OpenVAS等

#### 威胁建模

- 将信息搜集结果汇总至Mysql、SQLite、PostgreSQL

#### 漏洞分析

- Fuzz测试器
- Web应用漏洞探测分析模块
- 可挖0day

#### 后渗透攻击

- Meterpreter
  - 支持多操作系统
  - 驻留内存
  - 免杀
  - 提权
  - 信息提取
  - 监控
  - 跳板攻击
  - 内网扩展等

#### 报告生成

- 渗透测试结果可查询
- Pro版可导出不同类型报告

### 工具管理

#### 数据库

- 设置自动登录
  - `/usr/share/metasploit-framework/config/database.yml`
- 手动连接数据库
  - `service postgresql start`
  - `postgres psql`
  - `alter user postgres password 'adminp'`
  - `q`
- 设置账户认证方式
  - `vim /etc/postgresql/12/main/postgresql.conf`
  - 修改`password_encryption = md5`
  - `service postgresql restart`
  - `psql -U postgres -h 127.0.0.1` - 连接数据库
  - 新建数据库
    - `create user msf with password 'adminp' createdb;`
    - `create database msf with owner=msf;`
- `msfconsole`
- `db_status`查看数据库连接状态
  - 如果没有自动连接
  - 手动连接
    - `db_connect msf:adminp@127.0.0.1/msf`

### 命令参数

#### 核心命令

```shell
Command       Description
-------       -----------
?             帮助手册
banner        展示Metasploit框架信息
cd            改变当前工作目录
color         切换颜色（true|false|auto）
connect       远程连接-与主机通信
exit          退出Metasploit终端控制台
get           获取特定上下文变量的值
getg          获取一个全局变量的值
grep          grep另一个命令的输出
help          帮助手册
history       查看Metasploit控制台中使用过的历史命令
load          加载框架中的插件
quit          退出Metasploit终端控制台
repeat        Repeat a list of commands
route         Route traffic through a session
save          保存活动的数据存储
sessions      显示会话列表和有关会话的信息（sessions -h      列出sessions命令的帮助信息
sessions -i      查看所有的会话（基本信息）
sessions -v      列出所有可用交互会话及会话详细信息
sessions -i id   通过 ID 号，进入某一个交互会话
exit             直接退出会话
background       将会话隐藏在后台
sessions -K      杀死所有存活的交互会话）
set           设置一个特定的上下文变量（选项）的值
setg          设置一个全局变量的值
sleep         Do nothing for the specified number of seconds
spool         Write console output into a file as well the screen
threads       查看和操作后台线程
tips          Show a list of useful productivity tips
unload        卸载已加载框架插件
unset         取消设置的一个或多个特定的上下文变量
unsetg        取消设置的一个或多个全局变量的
version       查看框架和控制台库版本号
```

#### 模块命令

```shell
Command       Description
-------       -----------
advanced      显示一个或多个模块的高级（详细）选项
back          从当前上下文返回（退出当前正在使用的模块，返回原始控制台（模块的配置依然有效））
clearm        清除该模块的堆栈信息
info          显示有关一个或多个模块的信息
listm         显示该模块的堆栈信息
loadpath      从路径搜索并加载模块
options       显示一个或多个模块的全局选项信息（option|show option）
popm          将最新模块弹出堆栈并使其激活
previous      将先前加载的模块设置为当前模块
pushm         将活动模块或模块列表推入模块堆栈
reload_all    从所有定义的模块路径重新加载所有模块
search        搜索相关模块的名称和描述（search cve:2009 type:exploit platform:-linux）
show          查看显示给定类型的模块，或所有模块（show exploits|post|nop...）
use           装载一个渗透攻击或者模块
（use ModuleName    use exploit/windows/smb/ms17_010_eternalblue
info              查看模块的详细信息
options           查看脚本配置选项
show options      查看脚本配置选项
show targets      显示适用的主机类型
set               设置模块选项
run               启动脚本
exploit           启动脚本）
```

#### 作业命令

```shell
Command       Description
-------       -----------
handler       启动有效负载处理程序作为作业进程
jobs          查看和管理作业进程（查看和管理当前运行的模块）
kill          关闭|杀死一个作业进程
rename_job    重命名作业进程
```

#### 资源脚本命令

```shell
Command       Description
-------       -----------
makerc        将启动控制台以后要输入的命令保存到文件中（批处理文件）
resource      运行存储在文件中的命令（运行批处理文件）
```

#### 数据库后端命令

```shell
Command           Description
-------           -----------
analyze           分析有关特定地址或地址范围的数据库信息
db_connect        连接到现有的数据库服务（db_connect msf:adminp@127.0.0.1/msf）
db_disconnect     断开当前数据库服务
db_export         导出包含数据库内容的文件
db_import         导入扫描结果文件（将自动检测文件类型）
db_nmap           执行nmap并自动记录输出到数据库中（集成的nmap，对nmap的一个封装）
db_rebuild_cache  重建数据库存储的模块缓存（不建议使用）
db_remove         删除保存的数据库服务条目
db_save           将当前数据库服务连接保存为默认值，以便在启动时重新连接
db_status         显示当前数据库服务状态
hosts             列出数据库中的所有主机
loot              列出数据库中的所有战利品
notes             列出数据库中的所有注释
services          列出数据库中的所有服务
vulns             列出数据库中的所有漏洞
workspace         在数据库工作区之间切换
```

#### 凭证后端命令

```shell
Command       Description
-------       -----------
creds         列出数据库中的所有凭据
```

#### 开发者命令

```shell
Command       Description
-------       -----------
edit          使用首选编辑器编辑当前模块或文件
irb           在当前上下文中打开一个交互式Ruby Shell
log           如果可能，将framework.log显示到页面末尾（查看日志信息）
pry           在当前模块或框架上打开Pry调试器
reload_lib    从指定路径重新加载Ruby库文件
```

### 具体模块命令

#### auxiliary模块

```shell
Auxiliary Commands
==================
Command       Description
-------       -----------
check         检查目标是否存在漏洞
exploit       run命令的别名
rcheck        重新加载该辅助模块并检查目标是否存在漏洞
recheck       rcheck命令的别名
reload        重新加载该辅助模块（已配置的选项还在）
rerun         重新加载该辅助模块并运行该模块
rexploit      rerun命令的别名
run           运行选中的辅助模块
```

#### exploit模块

```shell
Exploit Commands
================
Command       Description
-------       -----------
check         检查目标是否存在漏洞
exploit       对目标发起攻击
rcheck        重新加载该辅助模块并检查目标是否存在漏洞
recheck       rcheck命令的别名
reload        重新加载该渗透攻击模块（已配置的选项还在）
rerun         rexploit命令的别名
rexploit      重新加载该渗透攻击模块并运行该模块对目标发起攻击
run           exploit命令的别名
```

#### payload模块

```shell
Payload Commands
================
Command       Description
-------       -----------
check         检查目标是否存在漏洞
generate      Generates a payload
reload        从磁盘重新加载当前模块
to_handler    创建具有指定有效负载的处理程序
```

