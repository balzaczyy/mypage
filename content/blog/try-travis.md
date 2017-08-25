---
title: 利用Travis做持续构建测试
date: '2014-10-08'
description:
categories:
- 技术
tags:

---

随着项目的规模不断增长，持续的构建测试能够有效的保障代码的质量。以前做Java的时候一直用Maven管理依赖，Jenkins自动化集成测试，Sonar监控代码质量。现在Go的项目，因为是放在Github上的关系，试用了下Travis。不得不说配置真心方便，yml几行代码就测试了Go从发布以来的四个版本（发现只支持到1.2+）。而且反应真的很灵敏，每次push代码，Travis都很勤恳的测试，有错误就发邮件通知我，搞的我现在每次push都很谨慎，生怕搞坏了build。

另外我还把构建的状态放到了Github项目的首页，看起来很专业嘛，嘻嘻。