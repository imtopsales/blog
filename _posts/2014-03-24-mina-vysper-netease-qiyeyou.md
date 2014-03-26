---
date: "2014-03-26 21:00:00 +0800"
layout: post
title: 试试自定义企业内部IM(基于apache vysper的xmpp服务+网易企业邮箱api)
categories: 2014-03
tags: mina vysper xmpp 网易企业邮箱
---


<div style="color:#dd0000;"><b>注意啊，我们也只是初步在这方面探讨了一下，并未真正用于实际工作环境中！</b></div>

<div style="margin-top: 25px;">现在市面上的企业IM软件非常多，大部分情况下够用有余了。但如果你喜欢自己掌控IM的源码，同时也有造轮子的习惯，也可以考虑像我们在这方面折腾一番。</div>

<div style="margin-top: 25px;"><b>折腾的目的</b></div>
<div>1) 初探基于开源XMPP的IM服务。</div>
<div>2) 基于企业邮箱API接口，把企业组织架构信息(公司通讯录)整合到XMPP服务中，无须另外管理IM的组织架构信息。</div>

<div style="margin-top: 25px;"><b>动手之前的几个前提条件：</b></div>
<div>1) 较熟悉java，能动手改代码(就是改<a target="_blank" href="http://mina.apache.org/vysper-project/index.html">Vysper</a>)。</div>
<div>2) 熟悉eclipse，或其他类似的ide，不过我后面的例子都是基于eclipse的。</div>
<div>3) 已经购买了网易企业邮箱。</div>

<div style="margin-top: 25px;"><b>好咯，可以开始折腾了，简单介绍一下步骤 (完整的代码见github：)</b></div>
<div><b>1)</b> 先去下载<a target="_blank" href="http://mina.apache.org/vysper-project/download_0.7.html">Vysper 0.7</a>，解压出来，放一边备用。</div>
<div><b>2)</b> 在eclipse中新建一个工程，新建lib文件夹，在上一步解压的文件中找出对应的jar包放到lib文件夹，加到build path；再把bogus_mina_tls.cert，log4j.xml，spring-config.xml这三个文件放到src文件夹中；另外，还需要找找httpclient的jar包，我用了4.3.1，可以根据实际需要在<a href="http://hc.apache.org/downloads.cgi" target="_blank">http://hc.apache.org/downloads.cgi</a>找找4.3.x的其他版本。</div>
<div><b>3)</b> 找网易企业邮箱的客服申请api权限，她们会提供一份文档的，文档里面有原理说明和api使用方法。然后我们需要给网易提供我们的服务器IP，另外还要生成一对rsa公私钥，公的给网易，私的留个自己。。。(网易客服邮箱 kf#qiye.163.com ，电话大概是400-6281-163)</div>
<div><b>4)</b> 接着到了改代码的环节，需要实现四个类。首先是账户相关的<code>UserService</code>；其次是部门组织架构相关的<code>RosterService</code>；然后实现一个<code>ProviderRegistry</code>(用于整合UserService和RosterService)；接着还少不了实现一个<code>NeteaseQiyeApi</code>，打包了本程序中需要用到的企业邮箱api。</div>
<div><b>5)</b> 最后还需要稍微改改spring-config.xml，把自己改的ProviderRegistry配置进去，还有前面生成的rsa私钥也要配置进去，明细见github的代码了。。</div>
<div><b>嗯，到此就完成了demo代码了，还算蛮简单的吧？嘿嘿！</b></div>

<div style="margin-top: 25px;"><b>附上两张eclipse工程的截图：</b></div>
<div style="overflow:hidden;"><img style="margin:0 0 3px 3px;float:left;" src="/media/img/201403/vysper.01.png" /><img style="margin:0 0 0 25px;float:left;" src="/media/img/201403/vysper.02.png" /></div>

<div style="margin-top: 25px;"><b>启动后端程序</b></div>
<div>执行项目源码中的org.apache.vysper.spring.ServerMain即可...</div>

<div style="margin-top: 25px;"><b>接着轮到客户端了，我们只用了pidgin来测试</b></div>
<div style="overflow:hidden;"><img style="margin:0 0 3px 3px;float:left;" src="/media/img/201403/vysper.03.png" /><img style="margin:0 0 0 25px;float:left;" src="/media/img/201403/vysper.04.png" /></div>
<div style="overflow:hidden;margin-top: 25px;"><img style="margin:0 0 3px 3px;float:left;" src="/media/img/201403/vysper.05.png" /><img style="margin:0 0 0 25px;float:left;" src="/media/img/201403/vysper.06.png" /></div>

<div style="margin-top: 25px;">嗯，目前就是这样的情况吧！</div>
