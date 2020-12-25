---
title: 用Linux或BSD使用PDAnet的最简单方法，实现无限制的连接
layout: post
image: https://i.imgur.com/wLMcNre.jpg
permalink: /cn/pdanet-linux-freebsd-unix
---

移动数据越来越便宜和更快，你可能有一个无限的4G / 5G在您的本地区域的报价。它通常会有一个陷阱，即严格限制数据分配的束缚，有时它是不允许的。

PDAnet](https://pdanet.co)是最简单的，也可能是最流行的方式来避免绑定数据上限。他们有一个适用于Windows和Mac OSX的应用程序，让你只需点击几下就可以进行连接。对于Linux、FreeBSD或Chrome OS用户来说，我们只能自己想办法了。

幸运的是，如果你的*nix电脑有一个工作的Wifi适配器，它不是那么困难的设置。

## ＃＃设置PDAnet你的手机

掌上网是可以通过Play Store、App Store获得的，所以你它的安装很直接。APK二进制文件](http://pdanet.co/install/)也可以在他们的官网上找到，以防你没有其他安装方式。

打开应用，然后点击**"WiFi直接热点（新！）"**的复选框，创建一个接入点。

然后你应该看到顶部的蓝色高亮文字。请注意**名称**和**密码**字段，因为它们总是随机生成的，所以你每次都要手动输入它们。

**我只用安卓系统进行了测试，但在iOS、Windows Phone或黑莓手机版本的应用中也可能是一样的。

## ＃＃在你的Linux/BSD盒子上设置WiFi。

使用你的WiFi网络管理器，搜索你随机生成的接入点，并使用应用程序中生成的密码连接到它。

然后，你会像正常的连接，但你仍然没有准备好浏览网页与正常的WiFi Tethering。一个HTTP代理将被托管在**http://192.168.49.1:8000**，你将只能通过它访问互联网。

## ＃＃浏览网络

如果您只需要使用网络浏览器，只需将代理设置为**192.168.49.1:8000**。

**在Firefox中**，进入**偏好->网络代理->设置**，并填写**手动代理**设置。

<pre>
  HTTP代理。192.168.49.1 

  端口：8000
</pre>

**对于Chromium或Chrome**，您将通过命令行设置代理。

<pre>
chromium-browser --proxy-server="192.168.49.1:8000"
</pre>

并且一定要检查**对所有协议使用此代理服务器**。

## ＃＃使用Apt-get(Apt)与PDAnet。

在基于Debian的发行版上，您可以通过设置代理设置来安装APT更新。

<pre>
  sudo nano /etc/apt/apt.conf.d/proxy.conf
</pre>

在**/etc/apt/apt.conf.d/proxy.conf**文件中添加这一行。

<pre>
  Acquire::http::Proxy "192.168.49.1:8000";
</pre>

保存**proxy.conf**文件。

## 使用PDAnet的代理链。

您可以通过proxychains强制程序使用您的PDA代理。

将您的服务器添加到**proxychains.conf**的末尾，删除文件中的其他服务器。

<pre>
  [代理清单]
  https 192.168.49.1 8000
</pre>

## ＃＃收尾

对于像我这样的旅行者来说，**PDAnet**是一个很好的工具，但试用版每隔15分钟就会断开连接，很烦人。除非你只需要短暂的、零星的绑定会话，否则完全值得购买15美元的许可证。

此外，**请不要滥用你的连接**与山洪，因为你永远不知道什么其他流量整形方法，你的运营商会雹下来对你。
