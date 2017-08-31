---
title: "Let's Encrypt"
date: 2017-08-31T23:22:16+08:00
---

首先上[成果](http://zhouyiyan.cn/letsencrypt.html)，页面自动切换到HTTPS，证书用的是Let's Encrypt的。整个过程还算顺利，首先用[http-server](https://github.com/indexzero/http-server)搭一个简单的HTTP服务器，配合[pm2](http://pm2.keymetrics.io/docs/usage/quick-start/)做成服务随系统启动，并在崩溃的时候重启服务。不过这么简单的一个HTTP服务器，应该不会死吧……

```bash
pm2 start hs --name="hs-80" -- /var/www -p 80
```

然后安装Let's Encrypt的[certbot](https://certbot.eff.org/#ubuntuxenial-other)。验证过域名以后，就会在/etc/letsencrypt下面存放账号和证书。这篇文档提到需要创建一个cron任务定时更新证书，但我感觉似乎默认已经有定时任务在运行了，所以我并没有做这一步。有了证书和秘钥就可以启动HTTPS服务器了。

```bash
pm2 start hs --name="hs-443" -- -S \
  -C /etc/letsencrypt/live/zhouyiyan.cn/fullchain.pem \
  -K /etc/letsencrypt/live/zhouyiyan.cn/privkey.pem \
  -p 443
```

尴尬的是certbot在安装好以后强烈建议我备份letscript那个配置目录，于是爱折腾的我，干脆配了Resilio Sync把整个目录同步了出来。过程也很简单，按照Resilio Sync的[Linux安装文档](https://help.resilio.com/hc/en-us/articles/206178924)和[Linux配置文档](https://help.resilio.com/hc/en-us/articles/204762449-Guide-to-Linux)搞好，在本地Mac上装一个客户端，对面加一个目录，然后这边贴一下key就搞定啦。

接下来就是看看三个月到了以后，证书能不能自动更新了。也许还要配服务器自动重启，额……
