---
title: 阻止运行、猎鹰网络、黑域 始末
date: 2017-01-26 16:21:12
updated: 2017-08-25 15:20:28
categories:
    - 异闻堂
tags:
    - Android
    - 省电
    - 黑域
    - 阻止运行
thumbnail: https://s.nfz.yecdn.com/img/thumbnails/forcestopgb-lieying-brevent.png!blogth
---
SuperSU 和阻止运行被收购和商业化无疑是一场巨变。因为 Root 和 Xposed 都是对 Android 安全、稳定运行非常重要的一部分，一旦商业化和作恶，后果不可预料。

<!--more-->

# ForceStopGB（阻止运行）

我来首先介绍一下阻止运行是什么。
阻止运行项目最早开始于 2015 年，原作者 liudongmiao 表示是写给他女朋友的一款作品，目的是为了遏制 Android 的众多毒瘤，通过 Xposed 或 Hook 系统 Framework 实现。项目完整地在 Github 上使用 WTFPL 协议完整开源并高度自由。截止到 2.3.2 版本，阻止运行已经是一款较完善的应用，名声广为流传，在酷安尤为口碑良好，甚至一度超过绿色守护。

# 被收购后的阻止运行

2016 年 3 月，liudongmiao 在酷安发表一条动态称，魔趣开源项目的发起人 Martincz 发现 ForceStopGB 项目在 Github 被删库，liudongmiao 表示阻止运行项目被卖给一家叫做“猎鹰工作室”的公司，并表示阻止运行即使被收购后依然不会作恶，并且 liudongmiao 表示阻止运行依然在他可控的范围之内。

> 后面大家可以看到，这一切并不是如 liudongmiao 所想的那样。

## 联网权限

猎鹰网络在收购发布的第一个版本 `2.3.3` 立刻就加入了联网权限，以及一个“立刻阻止”和“无法阻止？立刻上报程序猿”两个功能。猎鹰表示这个是必要权限。

> 2.3.3 的阻止运行的联网权限是否必要这里我已经不想深究。不然我备用机装一个 Xposed 再装一个抓包就全部找出来了。大家如果愿意的可以去尝试一下。

对于联网权限我想说一下，Xposed 是一把非常锋利的双刃剑，它的原理是通过替换 `/system/bin/app_process` 控制`zygote`，使 `app_process` 在启动过程中加载 `XposedBridge.jar`，从而完成对 `Zygote` 进程及其创建的 `Dalvik 虚拟机` `的劫持，Xposed 在开机的时候完成对所有的 Hook Function，在原 Function 执行的前后加上自定义代码。所以说，一般的权限管理软件对 Xposed Module 是毫无作用的，Xposed 无疑拥有系统的最高权限。

## 百度定位 SDK

这个猎鹰工作室的高振刚（即酷安中的 ksana2016）——猎鹰老大表示是上头公司要求内置的 sdk。至于上头公司是啥我后面会讲到。
最早发现这个的是因为一些酷友发现阻止运行 2.3.6 版开始莫名耗电，使用写轮眼一查看可以发现里面竟然内置了百度定位的 sdk `com.baidu.location.f` 。大家结合上面我介绍的 Xposed 的介绍，以及联系 Xposed 的后台保活能力，可以联想一下这个的后果。

> 其实大家想一下要定位权限有什么用？如果真的只是为了统计，为什么并没有在 `AndroidManiFest.xml` 内发现定义的其它统计有关的组件？而且，在酷友的强烈要求下，2.3.7 立刻就去掉了百度定位 sdk，说明这个组件对于应用运行是毫无影响的。

<img src="https://bbs-static.nfz.yecdn.com/i/0000056.png" alt="0000056.png" style="width:50%" />
<img src="https://bbs-static.nfz.yecdn.com/i/0000055.png" alt="0000055.png" style="width:50%" />

> 2.3.6 版本还可以在手机乐园上下载到，大家可以自取。

## 盗用 UI 设计

在 2.3.6，阻止运行使用了一个新的 UI 设计，包括一个 `listviewer` 和一个 `drawer`。然而很快，一名 ID 为 twroc 的酷友在酷安声称该 UI 设计所有权应归他所有，并且得到了 liudongmiao 的证实。然而猎鹰工作室对于此却宣称因为该酷友不肯加入猎鹰工作室的团队、不能接受“外包私活”等理由推诿。

> 这是酷友 tworc 的声明

<img src="https://bbs-static.nfz.yecdn.com/i/0000063.png" alt="0000063.png" style="width:50%" />
<img src="https://bbs-static.nfz.yecdn.com/i/0000051.jpg" alt="0000051.jpg" style="width:75%" />

最后这件事情是这样不了了之的。

<img src="https://bbs-static.nfz.yecdn.com/i/0000064.png" alt="0000064.png" style="width:50%" />

> 具体情况可以看下面

## 微阻止

这项功能当时 ksana2016 是这么介绍的：

<img src="https://bbs-static.nfz.yecdn.com/i/0000053.png" alt="0000053.png" style="width:50%" />

这项功能当时在酷安被大部分酷友抨击和反对。并且该功能在 2.4.0 版本终于推出以后，我们可以发现，所谓去除开屏广告不过是使广告不显示，实际上带有启动屏的广告应用启动时会有 2s 的黑屏。

# 猎鹰网络

猎鹰工作室到底是何方神圣？于是我上网进行了一番调查，结果很快就出来了。

这是搜狐新闻网的一篇[报道](http://mt.sohu.com/20150928/n422296570.shtml )，里面介绍了一个名叫“智度投资”的投资公司全资收购了猎鹰网络和半数“应用汇”的股份。

这是 [猎鹰网络的官网](http://www.falconnect.cn) ，可以在公司介绍里看到这样的内容：

> 猎鹰网络已成为国内领先的以大数据、机器学习、人工智能为技术驱动的新兴移动广告技术公司。

哦，一个有着“闭环生态链”的移动广告技术公司，要收购阻止运行这种对抗毒瘤的”安卓优化神器”，还要开发广告阻止功能？一旦借助 Xposed Hook 系统底层的优势投放广告、窃取用户隐私，是颇有些令人不寒而栗的，大家联想一下百度定位 SDK、联网权限应该也就明白了。

## 工作室成员行为和态度

### 面对盗用 UI 行为的态度

<img src="https://bbs-static.nfz.yecdn.com/i/0000057.png" alt="0000057.png" style="width:50%" />
<img src="https://bbs-static.nfz.yecdn.com/i/0000052.png" alt="0000052.png" style="width:50%" />

> 这脸打的 pia pia 的响。

<img src="https://bbs-static.nfz.yecdn.com/i/0000059.png" alt="0000059.png" style="width:50%" />

对于猎鹰高振刚和酷友 twroc 在微信的对话可以在[这里](https://ooo.0o0.ooo/2017/01/26/5889fb945e96e.jpg)看。

### 对于定位 SDK 的态度

<img src="https://bbs-static.nfz.yecdn.com/i/0000054.png" alt="0000054.png" style="width:50%" />

> 我不置可否，不过把质疑用户称为嘴脸也真是没谁了。

### 面对质疑的态度

> 如果你们的阻止运行的底线是这样，那么请问还有谁放心用？

<img src="https://bbs-static.nfz.yecdn.com/i/0000062.png" alt="0000062.png" style="width:50%" />

# 补丁版黑域

大概是这样的，liudongmiao 找到高振刚高总，申请开发基于 Android N 的补丁版“阻止运行”，即补丁版黑域项目。liudongmiao 表示新的项目只能用于 Android N、部分开源，并且不采用 Xposed 模式，于是高振刚同意了。后来补丁版黑域可以成功用于 Android 4.4-7.1 的任何版本，于是猎鹰网络威胁 liudongmiao 要起诉他。于是补丁版黑域被迫在酷安网下架，liudongmiao 被迫停更、去转向开发非补丁版黑域。

![0000050.png](https://bbs-static.nfz.yecdn.com/i/0000050.png)

幸运的是猎鹰网络没有（**实际上也没有能力**）封杀补丁版黑域，所以一键黑域打补丁项目和补丁版黑域依然可以继续使用。为了避免纠纷，酷安网页版隐藏了有关的项目，大家可以使用酷安手机客户端下载使用。

> 对我而言，我认为猎鹰网络起诉 liudongmiao 是无稽之谈。补丁版黑域仅仅使用了阻止运行闭源前 2.3.2 的源码（我自己也有一份，也开源在 Github 和 Coding 上），而且那份源码是根据 WTFPL 的协议开源的，是完全自由的。补丁版黑域的实现原理和阻止运行完全不同，无论是否支持 Android N 以下都无所谓。
> 猎鹰把一个本来开源的项目弄成闭源，还彻底毁了阻止运行，这样一个优秀开源项目的名声，谁的罪过更大一清二楚。

# 非补丁版黑域

现在非补丁版黑域使用了全新的实现方法，通过一定的权限（如 Priv 权限或者 ADB 权限）来监听 Android 的运行日志，获取应用自启、唤醒的情况，配合 Android N 的后台机制一起对付应用毒瘤。当然，这种方法并不是那么强力。

---

如果说，现在最终的结果绿色守护依然在不断完善，方便的 非补丁版黑域依然可以继续吊打毒瘤，补丁版黑域虽然不再提供支持、也依然可以使用，所以广大 Android 机油面对 BAT 毒瘤并不是没有方法。但是要说有什么损失，那么就是基于 Xposed 的一款开源自由的神器被迫闭源、走向了另一端，给大家留下一个商业化以后的反例。

----

# 黑域后续(更新于 2017.08.18)

> 这部分最早发布于[个人的 Telegram 频道](https://t.me/neoFelhzW)

黑域本身到底几宗罪？

最早宣称是为了自己的 Pixel 开发，不想 Root 和解锁，开发了基于 ADB 的黑域，然后开发了 Root 功能。
曾经宣称不对 Root 用户提供技术支持，然而 Root 模式需要捐赠才能使用（可惜我丢了那张 liudongmiao 骂捐赠用户是猪的截图，不然就太劲爆了）
认为绿色应用公约是没有意义的，认为只有比流氓技高一筹才能打败流氓。
liudongmiao 多次和绿色守护开发者冯老师针锋相对，多次恶意攻击 MyAndroidTools 和绿色守护的处方（你可以在他知乎上对“你如何看待绿色应用公约”问题的回答，含沙射影在攻击绿色守护的处方功能）
使用 WTFPL 开源了部分代码，但是却宣称任何人都无权分发第三方版本，甚至因为 Rikka 的 Shizuku Manager 参考了 Brevent Server 部分代码而大动肝火、在酷安怼人。如今又因为有人分发社区版而大动肝火，甚至拒绝开源部分代码；彻底违背了 WTFPL 的理念和意义，也玷污了开源这个名词。

liudongmiao 和冯老师之间的故事现在很像 SSR 和 SS，一个在努力宣称自己所谓的能力、对另一个针锋相对，另一个却在默默开发、努力提倡公约推动国内安卓生态的改变。
你国安卓生态会死于内讧，而不是死于 BAT。你国开源生态死于 liudongmiao 这样的人，而不是死于 妮哩萌萌 这样的人。

----

# 阻止运行后续(更新于 2017.08.25)

阻止运行已经被猎鹰工作室离职员工 “园子” 更名为 `绿色运行`，添加了所谓“游戏模式”——王者荣耀不卡顿。之前阻止运行多个版本均曝光了阻止运行劫持用户淘宝、强制给用户使用返利券、从而使工作室盈利的行为。为了自己的安全，请不要继续使用任何阻止运行（同样不推荐使用旧版本阻止运行）和绿色运行 Xposed 模块，也不要使用由猎鹰工作室或者推出的 Xposed 商店。当然，欢迎不怕死的人来作死。
