Freebuf 上面有篇文章“[如何防范Windows命令行工具遭黑客滥用](http://www.freebuf.com/articles/system/94675.html)”里面列举过黑客常用的 Windows 命令，但这篇文章只是列举了存在哪些命令，而本文则是详解这些命令的使用。

**0x00 渗透中常用的 Windows 命令**

本节首先来回顾下那篇文章中提及的常用 Windows 命令。

-   初步调查阶段：
    -   tasklist -- 显示运行的所有进程
    -   ver -- 显示系统版本号
    -   ipconfig -- 显示当前 TCP/IP 网络配置
    -   systeminfo -- 显示关于计算机及其操作系统的详细配置信息
    -   net time -- 查看系统时间
    -   netstat -- 显示网络连接、路由表和网络接口信息
    -   whoami -- 查看当前有效用户名
    -   net start -- 启动服务
    -   qprocess -- 显示 RD 会话主机服务器上正在运行的进程的相关信息
    -   query -- 显示进程、会话和 RD 会话主机服务器的相关信息
-   侦查阶段
    -   dir -- 显示磁盘目录内容
    -   net view -- 显示共享资源列表
    -   ping -- 检查网络是否连通
    -   net use -- 查看连接的计算机
    -   type -- 显示文本文件的内容
    -   net user -- 显示用户账户信息
    -   net localgroup -- 修改计算机上的本地组
    -   net group -- 添加、显示或修改服务器上的全局组
    -   net config -- 显示正在运行的可配置服务
    -   net share -- 创建、删除或显示共享资源
-   感染阶段
    -   at -- 计划任务
    -   reg -- 注册表操作
    -   wmic -- 提供了从命令行接口和批命令脚本执行系统管理的支持
    -   wusa -- 安装补丁
    -   netsh advfirewall -- 管理防火墙
    -   sc -- 用来和NT服务控制器和服务进行通讯的**命令**行程序
    -   rundll32 -- 调用动态链接程序库

**0x01 命令详解**

1.  **Net 命令**

**net view 命令**

[net view](https://technet.microsoft.com/en-us/library/hh875576(v=ws.11).aspx) 命令用于显示域列表、计算机列表或指定计算机的共享资源列表，格式如下：

net view [\\ComputerName [/CACHE] | [/ALL] | /DOMAIN[:DomainName]]

-   不带任何参数时，将显示当前域的计算机列表
-   \\ComputerName ： 用于查看指定共享资源的计算机
-   /CACHE： 显示当前系统中缓存的指定计算机上资源的客户端设置
-   /ALL： 显示所有共享包含 $shares
-   /DOMAIN[:DomainName]：用于查看指定的域，只使用参数 "/domain" 会显示当前网络中所有可用的域

**net user 命令**

[net user](https://technet.microsoft.com/en-us/library/cc771865(v=ws.11).aspx) 命令用于添加或更改用户账户或显示用户账户信息，该命令也可以写为 "net users"，格式如下：

net user [<UserName> {<Password> | *} [<Options>]] [/domain]  net user [<UserName> {<Password> | *} /add [<Options>] [/domain]]  net user [<UserName> [/delete] [/domain]]

-   不带任何参数时，显示计算机上所有的账户列表
-   <UserName>：用于添加、删除、更改或查看用户的账户名
-   <Password>：用于为用户账户分配或更改密码
-   /domain：用户在计算机主域的主域控制器中执行操作

**net localgroup 命令**

[net localgroup](https://technet.microsoft.com/en-us/library/cc725622(v=ws.11).aspx) 命令用于修改计算机上的本地组，格式如下：

net localgroup [<GroupName> [/comment:"<Text>"]] [/domain]  net localgroup [<GroupName> {/add [/comment:"<Text>"] | /delete} [/domain]  net localgroup [<GroupName> <Name> […] {/add |  /delete} [/domain]

-   不带任何参数时，显示计算机上的本地组。
-   <GroupName>：表示需要添加、扩充或删除的本地用户组
-   [/comment:"<Text>"]：表示为新建或现有的组添加注释
-   /domain：表示在当前域的主域控制器上执行操作，否则在本地计算机上执行这个操作
-   <Name> […]：列出一个或多个需要从一个本地组中添加或删除的用户名或组名。可以用空格来将多个用户名分隔开。名字可以是用户或全局组，但不可以是其它的本地组。如果一个用户来自另 外一个域，就应在用户名前加上域名(例如 SALES\RALPHR)
-   /add：用于将全局组名或用户名添加到本地组中
-   /delete：用于从本地组中删除组名或用户名

**net use 命令**

[net use](https://technet.microsoft.com/en-us/library/gg651155(v=ws.11).aspx) 命令用于查看连接的计算机，断开计算机与共享资源的连接，或者显示计算机的连接信息，格式如下：

net use [{<DeviceName> | *}] [\\<ComputerName>\<ShareName>[\<volume>]] [{<Password> | *}]] [/user:[<DomainName>\]<UserName>] [/user:[<DottedDomainName>\]<UserName>] [/user: [[UserName@DottedDomainName](mailto:UserName@DottedDomainName)] [/savecred] [/smartcard] [{/delete | /persistent:{yes | no}}]  net use [<DeviceName> [/home[{<Password> | *}] [/delete:{yes | no}]]  net use [/persistent:{yes | no}]

-   不带任何参数时，显示网络连接
-   <DeviceName>：用于指定要连接的资源名称或要断开的设备名称
-   \\<ComputerName>\<ShareName>：表示服务器及共享资源的名称
-   <Password>：表示访问共享资源的密码
-   /user：用于指定进行连接的另一个用户
-   <DomainName>：用于指定另一个域
-   <UserName>：指定登录的用户名
-   /home：用于将用户连接到主目录
-   /delete：用于取消指定的网络连接
-   /persistent: {yes | no}：用于控制持久网络连接的使用。默认值为最后一次使用的设置。非设备连接不会持久。Yes 将按其建立时的原样保存所有连接，并在下次登录时还原它们。No 则不保存已建立的连接或后续连接。现存的连接在下一次登录时还原。使用 /delete 删除持久连接。

**net time 命令**

[net time](https://technet.microsoft.com/en-us/library/bb490716.aspx) 命令用于查看系统时间，使计算机的时钟与另一台计算机或域的时钟同步，格式如下：

net time [{\\ComputerName | /domain[:DomainName] | /rtsdomain[:DomainName]}] [/set]  net time [\\ComputerName] [/querysntp] [/setsntp[:NTPServerList]]

-   \\ComputerName：表示要检查或同步的服务器名
-   /domain[:DomainName]：指定要与其时间同步的域
-   [/set]：用于是本计算机始终与指定计算机或域的时钟同步

**net share 命令**

[net share](https://technet.microsoft.com/en-us/library/hh750728(v=ws.11).aspx) 命令用于创建、删除或显示共享资源，格式如下：

net share <ShareName>  net share <ShareName>=<drive>:<DirectoryPath> [/grant:<user>,{read | change |full}] [/users:<number> | /unlimited] [/remark:<text>] [/cache:{manual | documents | programs | BranchCache |none} ]  net share [/users:<number> | /unlimited] [/remark:<text>] [/cache:{manual | documents | programs | BranchCache |none} ]  net share {<ShareName> | <DeviceName> | <drive>:<DirectoryPath>} /delete  net share <ShareName> \\<ComputerName> /delete

-   不带任何参数时，显示本地计算机上所有共享资源的信息
-   <ShareName>：表示共享资源的网络名称
-   <drive>:<DirectoryPath>：用于指定共享目录的绝对路径
-   /users:<number>：用于设置可同时访问共享资源的最大用户数
-   /unlimited：表示不限制同时访问共享资源的用户数
-   [/remark:<text>]用于添加关于资源的注释，注释文字用引号包含

**net group 命令**

[net group](https://technet.microsoft.com/en-us/library/cc754051(v=ws.11).aspx) 命令用于添加、显示或修改服务器上的全局组，格式如下：

net group [<GroupName> [/comment:"<Text>"]] [/domain]  net group [<GroupName>{/add [/comment:"<Text>"] | /delete} [/domain]]  net group [<GroupName> <UserName>[ ...] {/add | /delete} [/domain]]

-   不带任何参数时，显示服务器上的组名
-   <GroupName>：指需要添加、扩充或删除的组的名称
-   [/comment:"<Text>"]：为一个新的或已存在的组添加注释
-   [/domain]：在当前域的主域控制器上执行操作
-   <UserName>[ ...]：列出一个或多个需要从一个组中添加或删除的用户名
-   /add：添加一个组，或将一个用户名添加到一个组中
-   /delete：删除一个组，或将一个用户名从一个组中删除

**net config 命令**

[net config](https://technet.microsoft.com/en-us/library/bb490700.aspx) 命令显示正在运行的可配置服务，或显示和更改服务器服务或工作站服务的设置，格式如下：

net config [{server|workstation}]xxxxxxxxxx

-   server：在运行服务器服务时，显示其设置并允许更改该设置
-   workstation：在运行工作站服务时，显示其设置并允许更改该设置

1.  **Tasklist 命令**

[tasklist](https://technet.microsoft.com/en-us/library/bb491010.aspx) 命令用来显示运行在本地或远程计算机上的所有进程，格式如下：

tasklist[.exe] [/s computer] [/u domain\user [/p password]] [/fo {TABLE|LIST|CSV}] [/nh] [/**fi** FilterName [/**fi** FilterName2 [ ... ]]] [/m [ModuleName] | /svc | /v]

-   [/s computer]：指定连接到的远程系统(IP)
-   /u domain\user：指定使用哪个用户执行这个命令
-   [/p password]：为指定的用户指定密码
-   [/fo {TABLE|LIST|CSV}]：指定输出格式，有效值为"TABLE"、"LIST"、"CSV"
-   [/nh]： 指定栏标头不应该在输出中显示，只对 "TABLE" 和 "CSV" 格式有效
-   /m [ModuleName ] :列出调用指定的 DLL 模块的所有进程，如果没有指定模块名，显示每个进程加载的所有模块
-   /svc：显示每个进程中的服务
-   /v：指定要显示详述信息

1.  **Ipconfig 命令**

[ipconfig](https://technet.microsoft.com/en-us/library/dd197434(v=ws.11).aspx) 命令用于显示所有当前的 TCP/IP 网络配置值、刷新动态主机配置协议 (DHCP) 和域名系统 (DNS) 设置，格式如下：

ipconfig [/allcompartments] [/all] [/renew [<Adapter>]] [/release [<Adapter>]] [/renew6[<Adapter>]] [/release6 [<Adapter>]] [/flushdns] [/displaydns] [/registerdns] [/showclassid <Adapter>] [/setclassid <Adapter> [<ClassID>]]

-   不带任何参数时，显示所有适配器的 IP 地址、子网掩码、默认网关
-   /all：显示所有适配器的完整 TCP/IP 配置信息
-   /renew [<Adapter>]：更新所有适配器 ( 如果未指定适配器 ) ，或特定适配器 ( 如果包含了 adapter 参数 ) 的 DHCP 配置， 该参数仅在具有配置为自动获取 IP 地址的网卡的计算机上可用
-   /release [<Adapter>]： 发送 DHCPRELEASE 消息到 DHCP 服务器，以释放所有适配器 ( 如果未指定适配器 ) 或特定适配器 ( 如果包含了 adapter 参数 ) 的当前 DHCP 配置并丢弃 IP 地址配置
-   /flushdns：清理并重设 DNS 客户解析器缓存的内容
-   /displaydns： 显示 DNS 客户解析器缓存的内容， 包括从本地主机文件预装载的记录以及由计算机解析的名称查询而最近获得的任何资源记录
-   /registerdns：初始化计算机上配置的 DNS 名称和 IP 地址的手工动态注册
-   /showclassid <Adapter>：显示指定适配器的 DHCP 类别 ID ，要查看所有适配器的 DHCP 类别 ID ，可以使用星号 (*) 通配符代替 adapter
-   /setclassid <Adapter> [<ClassID>]：配置特定适配器的 DHCP 类别 ID 。 要设置所有适配器的 DHCP 类别 ID ，可以使用星号 (*) 通配符代替 adapter ，该参数仅在具有配置为自动获取 IP 地址的网卡的计算机上可用，如果未指定 DHCP 类别的 ID ，则会删除当前类别的 ID

1.  **Systeminfo 命令**

[systeminfo](https://technet.microsoft.com/en-us/library/cc771190(v=ws.11).aspx) 命令显示关于计算机及其操作系统的详细配置信息，包括操作系统配置、安全信息、产品 ID 和硬件属性，格式如下：

Systeminfo [/s <Computer> [/u <Domain>\<UserName> [/p <Password>]]] [/fo {TABLE | LIST | CSV}] [/nh]

-   不带任何参数时，显示操作系统的详细配置信息
-   /s <Computer>：指定远程计算机名称或IP地址，默认值是本地计算机
-   /u <Domain>\<UserName>：使用 UserName 或 Domain\UserName 指定的用户帐户权限运行该命令
-   /p <Password>：对应 \u 指定用户的密码
-   [/fo {TABLE | LIST | CSV}]：指定输出格式，有效值为"TABLE"、"LIST"、"CSV"
-   [/nh]：指定栏标头不应该在输出中显示，只对 "TABLE" 和 "CSV" 格式有效

1.  **Netstat 命令**

[netstat](https://technet.microsoft.com/en-us/library/ff961504(v=ws.11).aspx) 命令用于显示网络连接、路由表和网络接口信息，格式如下：

Netstat [-a] [-e] [-n] [-o] [-p <Protocol>] [-r] [-s] [<Interval>]

-   a：显示所有socket，包括正在监听的
-   e：显示以太网统计信息。此选项可以与 -s 选项组合使用
-   n：以数字形式显示地址和端口号
-   o：显示与每个连接相关的所属进程 ID
-   [-p <Protocol>]：显示 protocol 指定的协议的连接，protocol 可以为 "TCP"、"UDP"、"TCPv6"和"UDPv6"
-   r：显示路由表
-   s：显示按协议统计信息
-   <Interval>：重新显示选定统计信息，每次显示之间暂停时间间隔(以秒计)

1.  **Dir 命令**

[dir](https://technet.microsoft.com/en-us/library/cc755121(v=ws.11).aspx) 命令用于显示磁盘目录的内容，格式如下：

dir [<Drive>:][<Path>][<FileName>] [...] [/p] [/q] [/w] [/d] [/a[[:]<Attributes>]][/o[[:]<SortOrder>]] [/t[[:]<TimeField>]] [/s] [/b] [/l] [/n] [/x] [/c] [/4]

-   [<Drive>:][<Path>][<FileName>]：盘符 路径 文件名
-   /p：表示分屏显示，屏幕上一次显示32行文件信息，然后暂停并提示“请按任意键继续”
-   /q：显示所有者信息
-   /w：以宽格式显示列表，在每一行上最多显示 5 个文件名或目录名
-   /d：与 /w 相同，但是文件按列排序
-   /a[[:]<Attributes>]：只显示那些指定属性的目录和文件名称，如果在没有指定 attributes 的情况下使用 /a，dir 显示所有文件的名称，包括隐藏文件和系统文件
-   /o[[:]<SortOrder>]：控制 dir 排序和显示目录名和文件名的顺序，如果在没有指定 SortOrder 的情况下使用 /o，dir 显示按字母顺序排列的目录名，然后显示按字母顺序排列的文件名
-   /t[[:]<TimeField>]：指定显示或用于排序的时间字段
-   /s：列出指定目录及所有子目录中出现的每个指定的文件名
-   /b：列出每个目录名或文件名
-   /l：按小写字母显示未排序的目录名和文件名
-   /n：显示长列表格式，文件名在屏幕最右边
-   /x：显示 NTFS 和 FAT 卷上文件生成的短名称
-   /c：按文件大小显示多个分隔符
-   /4：显示四位数字的年份格式

1.  **At 命令**

[at](https://technet.microsoft.com/en-us/library/cc772590(v=ws.11).aspx) 命令用于计划在指定时间和日期在计算机上运行命令和程序，格式如下：

at [\\ComputerName] [{[ID] [/delete] | /delete [/yes]}]  at [[\\ComputerName] Hours:Minutes [/interactive] [{/every:Date[,...] | /next:Date[,...]}] Command]

-   ComputerName：指定远程计算机。如果省略该参数，则 at 计划本地计算机上的命令和程序
-   ID：指定指派给已计划命令的识别码
-   /delete：取消已计划的命令。如果省略了 ID，则计算机中所有已计划的命令将被取消
-   /yes：删除已计划的事件时，对来自系统的所有询问都回答“是”
-   Hours:Minutes：指定命令运行的时间，该时间用 24 小时制
-   /interactive：对于在运行 command 时登录的用户,允许 command 与该用户的桌面进行交互
-   /every:Date：在每个星期或月的指定日期运行命令
-   /next：下一个指定日期运行命令