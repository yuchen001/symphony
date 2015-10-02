# Symphony [![Build Status](https://img.shields.io/travis/b3log/symphony.svg?style=flat)](https://travis-ci.org/b3log/symphony)

## 简介

Sym 是一个用 Java 写的实时论坛，欢迎来[体验](http://hacpai.com/register?r=Vanessa)！


### 初衷

Sym 的诞生是有如下几点原因：

* 我们想实现一种新的网络社区体验，独立博客+社区互动
* 大多数论坛用户体验不够现代化，想做一个和聊 QQ 一样体验的论坛
* 已有的用 Java 写的论坛真的很少/丑，并且大多已经不再维护

### 基本理念

#### 实时交互

在浏览帖子时，传统论坛都是需要刷新页面来查看回帖的。Sym 在类似的用户交互场景上是基于 WebSocket 技术进行架构的，看帖时不需要刷新页面也可以看到其他人回帖。

#### HTML5

Sym 使用了很多 HTML5 提供的技术特性，比如通过使用_本地存储_防止编辑帖子/评论时内容丢失；使用了_音频_特性来进行帖子/评论音频录制；复制/粘贴上传图片等等。

运用这些技术，Sym 可以让用户在分享、灌水时更加便捷、舒服 :smirk: 

#### 积分系统

积分系统是所有论坛的基础/标配系统之一吧，好玩是一方面，另一方面是量化每个用户的价值。Sym 的积分系统参考了 [V2EX](http://v2ex.com) 的积分系统，未来将会加入更多动态特性，比如用户阵营汇率、系统运营参数等。

#### 互联

Sym 提供了 API 进行帖子、评论的同步（[B3log 构思](http://hacpai.com/b3log)），目前 [Solo](https://github.com/b3log/solo) 博客系统已经可以完整和 Sym 保持内容同步。

### 功能图解

**首页**

首页使用 Reddit 热帖排序算法，基于用户投票和时间来决定首页内容。另外，列表上面的每篇帖子都有一个_小红条_，表示该帖的当前热度（实时浏览/评论）。

![首页](https://cloud.githubusercontent.com/assets/873584/10239677/db41be9e-6903-11e5-9a93-d095c62fe103.png)

**帖子**

![帖子](https://cloud.githubusercontent.com/assets/873584/10239706/4d98c668-6904-11e5-8c1d-3ca9e5d1584a.png)

**个人设置**

![个人设置](https://cloud.githubusercontent.com/assets/873584/10239055/23c48c32-68fa-11e5-857d-11b82941810a.png)

**发布选择**

目前有 4 类帖子：

* 文章：普通的帖子，注重作者分享经验和见解
* 思绪：记录写作过程，实例请看[这里](http://hacpai.com/article/1442568741454)
* 讨论组：邀请好友进行私密交流，其他用户看不到具体内容和评论
* 同城广播：发起你所在城市的招聘、Meetup 等

![发布选择](https://cloud.githubusercontent.com/assets/873584/10239716/6ebcf5f8-6904-11e5-9f7c-e16cd5afe0ac.png)

**发布编辑**

* Markdown 编辑器
* Chrome 下可以直接粘贴图片，其他浏览器支持拖拽
* 除了使用文字，也可以在帖子内一键进行录音
* 支持标准 Emoji 表情
* 积分打赏

![发布编辑](https://cloud.githubusercontent.com/assets/873584/10239755/ed2ca5f0-6904-11e5-8945-1a2a2ec11e69.png)

#### 移动端

移动端目前除了不能录音外，其他功能和 PC 端保持一致。

**首页**
![移动端首页](https://cloud.githubusercontent.com/assets/873584/10241975/e719d4ce-691f-11e5-9336-1df33e11425a.png)

**浏览帖子**
![移动端浏览帖子](https://cloud.githubusercontent.com/assets/873584/10242407/279d2ba6-6923-11e5-9265-62afbd024c0b.png)

**评论区**
![移动端评论区](https://cloud.githubusercontent.com/assets/873584/10242536/02d08358-6924-11e5-94c5-8ea10e1c7c8d.png)

**发布**
![移动端发布](https://cloud.githubusercontent.com/assets/873584/10241983/f0f1e248-691f-11e5-80c2-16fbda989da9.png)

## 安装

需求：Maven3+、MySQL5+、Jetty9+

1. [下载](https://github.com/b3log/symphony/archive/master.zip)源码
2. 解压后修改 `src/main/resources/local.properties` 中的数据库配置，并创建数据库
3. _可能需要_修改 `latke.properties` 中的端口为容器端口
4. _可能需要_修改 `init.properties` 中的管理员账号
3. 使用 `mvn install` 进行构建
4. 部署到 Servlet 容器的 ROOT 下并启动容器，数据库表会在第一次启动时自动建立

注意：

* 只能部署到 ROOT 中，线上环境建议使用反向代理

## 配置

* 图片上传使用的是[七牛](http://www.qiniu.com)，需要配置 `symphony.properties` 中的 `qiniu.*` 属性
* 邮件发送使用的是 [SendCloud](http://sendcloud.sohu.com)，需要配置 `symphony.properties` 中的 `sendcloud.*` 属性

用户注册时是启用邮件验证的，如果需要修改请参考相关代码。

## 商用授权

请看[这里](https://github.com/b3log/symphony/wiki/%E5%95%86%E7%94%A8%E6%8E%88%E6%9D%83)。

## 思绪

在实现 [B3log 构思](http://hacpai.com/b3log)的这几年：

* 我们见证了 xAE（GAE/BAE/SAE/etc）的兴起与没落。2009 年选择了 GAE 作为服务器，并开始实现 Latke 框架来解决跨云平台，直到今年[告别 GAE](http://hacpai.com/article/1443685401909)，不得不感叹技术更迭之快
* 感受到了自造轮子的优缺点，并且可以肯定一点：对于一个想要长久的产品来说，自制技术框架优势远大于劣势
* 一个_好玩_的产品或说是细节特性然并卵，需要做的是一个能够持续提供用户价值的产品/特性
* 虽然直到目前 B3log 系产品用户不多，但我们已经初步证明了：Java 用来实现博客、论坛没有什么不好的（仅次于 PHP 吧）
* 先完成本职工作，再用开源的产品/经验来进行工作相关结合与提升

## Terms

* This software is open sourced under the Apache License 2.0
* You can not get rid of the "Powered by [B3log 开源](http://b3log.org)" from any page, even which you made
* If you want to use this software for commercial purpose, please mail to support@liuyun.io for a commercial license request
* Copyright &copy; b3log.org, all rights reserved

