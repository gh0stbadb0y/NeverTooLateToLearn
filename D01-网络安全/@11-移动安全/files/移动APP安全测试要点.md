
[](http://blog.nsfocus.net/mobile-app-security-security-test/)[http://blog.nsfocus.net/mobile-app-security-security-test/](http://blog.nsfocus.net/mobile-app-security-security-test/)

**移动APP安全测试要点** 上次《 [运营商渗透测试与挑战](http://blog.nsfocus.net/the-challenge-in-penetration-test-for-isp/)》中提到，随着运营商新技术新业务的发展，运营商集团层面对安全的要求有所变化，渗透测试工作将会面临内容安全、计费安全、客户信息安全、业务逻辑及APP等方面的挑战。随着运营商自主开发的移动APP越来越多，这些APP可能并不会通过应用市场审核及发布，其中的安全性将面临越来越多的挑战，这一点在《 [XcodeGhost危害国内苹果应用市场](http://blog.nsfocus.net/xcodeghost-harm-third-party-appstore/)》一文中就曾提到过。

这个问题也引起了运营商的足够重视，已经自主开发了自动化检测工具及定期的APP安全测试评估工作。在此，绿盟科技博客特别邀请到移动APP安全测试专家，让他们结合一次Android APP安全测试实例，为大家讲解评估特点，并将评估检查点、评估细节和整改建议一一列出，给大家提供移动终端APP安全测试的思路。

作者：侯绍岗 杨乔国

## 评估思路

### 移动APP面临的威胁

风起云涌的高科技时代，随着智能手机和iPad等移动终端设备的普及，人们逐渐习惯了使用应用客户端上网的方式，而智能终端的普及不仅推动了移动互联网的发展，也带来了移动应用的爆炸式增长。在海量的应用中，APP可能会面临如下威胁：

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/66f1e93d-fd86-48f7-96ff-1001906694aa/image001.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/66f1e93d-fd86-48f7-96ff-1001906694aa/image001.png)

### 新技术新业务移动APP评估思路

在这次的移动APP安全测试实例中，工作小组主要通过如下7个方向，进行移动终端APP安全评估：

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2a169164-9575-4deb-acb2-478c474813c5/image003.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2a169164-9575-4deb-acb2-478c474813c5/image003.png)

### 运营商自动化APP测评思路

运营商自主开发的自动化APP安全检测工具，通过”地、集、省”三级机构协作的方式，来完成移动终端APP安全检测与评估。APP测试思路如下：

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4c88f22b-3d78-434a-aa35-df03d3dba871/image004.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4c88f22b-3d78-434a-aa35-df03d3dba871/image004.png)

## 安全检测要点

### Allowbackup漏洞

AndroidManifest.xml文件中allowBackup属性值被设置为true。当allowBackup标志为true时，用户可通过adb backup来进行对应用数据的备份，在无root的情况下可以导出应用中存储的所有数据，造成用户数据的严重泄露。

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04e45019-7502-4c92-bed6-95be9b3ece1d/image006.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04e45019-7502-4c92-bed6-95be9b3ece1d/image006.png)

**整改建议**

将参数android:allowBackup属性设置为false，不能对应用数据备份。

### WebView漏洞

应用中存在WebView漏洞，没有对注册JAVA类的方法调用进行限制，导致攻击者可以利用反射机制调用未注册的其他任何JAVA类，最终导致javascript代码对设备进行任意攻击。

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f7856f9c-26b6-4e63-97c4-803ce3671e38/image008.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f7856f9c-26b6-4e63-97c4-803ce3671e38/image008.png)

**整改建议**

通过在Java的远程方法上面声明一个@JavascriptInterface 来代替addjavascriptInterface；

在使用js2java的bridge时候，需要对每个传入的参数进行验证，屏蔽攻击代码；

**Note ：控制相关权限或者尽可能不要使用js2java 的bridge 。**

### 关键数据明文传输

应用程序在登录过程中，使用http协议明文传输用户名和密码，并未对用户名和密码进行加密处理。通过监控网络数据就可以截获到用户名和用户密码数据，导致用户信息泄露，给用户带来安全风险。

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/17cbb881-dede-4b6b-b3b4-974afec4c160/image010.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/17cbb881-dede-4b6b-b3b4-974afec4c160/image010.png)

**整改建议**

在传输敏感信息时应对敏感信息进行加密处理。

### 任意账号注册

使用手机号133*****887注册某个APP，获取验证码46908；

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8620aae7-c92b-4f1c-a2c9-f334a75be88e/image011.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8620aae7-c92b-4f1c-a2c9-f334a75be88e/image011.png)

在确认提交时，拦截请求，修改注册的手机号码，即可注册任意账号，这里修改为1338*****678（任意手机号）；

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/46f264dc-cea9-4e82-819c-9d00b5807a60/image013.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/46f264dc-cea9-4e82-819c-9d00b5807a60/image013.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0140d857-1d26-4d4e-a92d-32fc152c5380/image014.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0140d857-1d26-4d4e-a92d-32fc152c5380/image014.png)

分别使用133_****887和133****_678（任意手机号）登录，均可以通过验证登录，看到最终结果。

**整改建议**

注册过程最后的确认提交时，服务器应验证提交的账号是否是下发验证码的手机号。

### 登录界面可被钓鱼劫持

应用存在钓鱼劫持风险。应用程序没有做防钓鱼劫持措施，通过劫持应用程序的登录界面，可以获取用户的账号和密码，可能导致用户账号信息的泄露。

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3fb51a7e-f586-4b4f-8182-1c2be2a8a626/image021.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3fb51a7e-f586-4b4f-8182-1c2be2a8a626/image021.png)

**整改建议：**

应用程序自身通过获取栈顶activity，判断系统当前运行的程序，一旦发现应用切换（可能被劫持），给予用户提示以防范钓鱼程序的欺诈。

获取栈顶activity（如下图），当涉及敏感activity（登录、交易等）切换时，判断当前是否仍留在原程序，若不是则通过Toast给予用户提示。

使用HTML5架构或android+HTML5混合开发，实现登陆、支付等关键页面，降低被劫持的风险。

## 有争议的整改建议

在实施整改过程中，运营商、APP厂商及安全厂商之间就如下几点存在争议：

### 关键数据明文传输

根据客户测评结果以及移动终端APP厂商理解，目前的数据安全问题可为：

-   客户端安全（数据录入）。
-   客户端到服务器安全（数据传输）。
-   服务器端安全（数据存储）。

而关键数据明文传输属于客户端数据录入安全，针对此部分，目前不仅是移动终端APP，包括Web安全方面，对此部分要求也是不一而分，具体可以体现为：

-   **具有现金流的交易平台：** 此类业务安全级别要求最高，在数据传输方面也是目前做得最好的。主要代表是：淘宝、京东、各大银行网银等。
-   **具有较大社会影响力的平台：** 此类业务安全级别低于上述业务，但由于账户数据丢失以后，对其自身以及社会影响较大，所以在传输上也不会采取明文传输。如：百度、腾讯等。
-   **数据丢失本身不会造成较大的影响的平台：** 此类业务账户数据本身价值不大，丢失以后也不会造成影响，或者本身不会受到太大关注，一般都不会对传输数据进行加密。这样的例子比比皆是。

当然也有厂商提出，明文传输在某些专业的漏洞检测和通报的网站上，是不属于安全漏洞的，为了验证此异议，在某平台上提交了一份关于明文传输的漏洞，得到的结果请看下图：

### 登录界面钓鱼劫持

APP应用存在钓鱼劫持风险。应用程序没有做防钓鱼劫持措施，通过劫持应用程序的登录界面，可以获取用户的账号和密码，可能导致用户账号信息的泄露。

这一条检测结果，最大的争议在于按照整改建议整改以后，对一般用户来说，没有任何作用。首先，我们了解一下钓鱼劫持如何产生。

**Android钓鱼原理**

需要理解，Android启动一个Activity时，是这样设计的，给Activity加入一个标志位FLAG_ACTIVITY_NEW_TASK，就能使它置于栈顶并立马呈现给用户。但是这样的设计却有一个缺陷。如果这个Activity是用于盗号的伪装Activity呢？这种现象在XcodeGhost事件中，已经被证实是可以实现的。

在Android系统当中，程序可以枚举当前运行的进程而不需要声明其他权限，这样的话，就可以编写一个程序，启动一个后台的服务，这个服务不断地扫描当前运行的进程，当发现目标进程启动时，就启动一个伪装的Activity。如果这个Activity是登录界面，那么就可以从中获取用户的账号密码，具体的过程如下图：

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6c4f7eaa-86ef-43bc-a329-7cd017e78012/image027.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6c4f7eaa-86ef-43bc-a329-7cd017e78012/image027.png)

检测原理描述清楚以后，就需要给出让软件厂商能够明白的整改建议以及漏洞情景重现。

**Android钓鱼情景演示**

以小米手机为例：

1.当打开3个APP时，最后一个打开的APP”语音助手”，切换至手机桌面，长按HOME键查看进程，”语音助手”会显示在进程的第一个。

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dff1ec74-fc5a-4588-8543-d0822a8adca5/image029.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dff1ec74-fc5a-4588-8543-d0822a8adca5/image029.png)

2.点击”微信”以后，切换至”微信”，再查看进程，可以看到，进程中由于”微信”已切换至当前窗口，故进程中不存在。

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6d89e6ec-cd5f-47ef-8276-02791e4cd908/image030.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6d89e6ec-cd5f-47ef-8276-02791e4cd908/image030.png)

3.可以从第1步看到，当切换至手机桌面时，无论是语音助手、手机令牌、还是微信，都是默认后台运行，而且切换出来以后无任何提示。这样，当恶意activity收到微信登录界面或者其他敏感界面的时候，就会抢先推送至客户，从而让客户轻易的输入了帐号，并获取了客户的信息，但此时微信不会做任何提示。

4.再来观看一下某行手机APP，当切换至手机桌面时，会对客户做出提示。如下图：

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8b4156e9-9b10-4ac7-a973-bca9d0a40262/image031.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8b4156e9-9b10-4ac7-a973-bca9d0a40262/image031.png)

假设一下页面是恶意推送的activity，那么在恶意推送的APP页面，应该会显示出此类提示，告知客户，此页面并非正常APP的页面。

用户打开正常页面 vs 用户打开了恶意页面

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/27d6065f-0323-4256-b60a-1d61bda65fe3/image033.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/27d6065f-0323-4256-b60a-1d61bda65fe3/image033.png)

## 总结

从工信部《新技术新业务信息安全评估管理办法（试行）》（工信部保〔2012〕117号)及运营商的相关文件规定，以及绿盟科技实施的移动APP安全测试项目来看，移动APP安全测试在运营商的重要地位。

本文通过对一次移动APP安全测试及评估的实际案例，希望能够对安全从业者在移动终端APP评估方面，也欢迎大家在QQ群里参与这方面的讨论。