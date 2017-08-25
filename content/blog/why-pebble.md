---
title: Why Pebble
date: '2012-10-23'
description:
categories:
- 技术
tags:
- pebble
---

Sometime I'm asking myself, why I chose Pebble at the first time? I already had Wordpress as my blogging software. It's a lot easier to go with WP, instead of fooling around the Pebble, right?

The truth is that, I'm not a pure blogger. I'm a developer. I need something as my pet project, which is more free from legal restriction, more free to use cutting edge technologies, and more fun to do so. I could have chosen some fancy iOS app. In fact, I did finish 31 days app learning series, and created one prototype for Lotus iNotes offline client, which I hoped to overcome the bad performance and experiences I had with my company's mail client. However, it didn't work for me, since my day job didn't give me much time and the management team was not very interested in it either. Anyway, I have to choose something I'm more familiar with.

Blogging software seems to be a good choice. It's kinda like content management system, which is closer related to my day job. And Pebble is the first open source Java based blogging software I found. It is full featured, and  seems to beat other Java based opponents around 2010. Though it stopped active development since mid-2011, it's still a perfect candidate for me.

I still call it Pebble but it doesn't share much with its origin and will sooner or later be changed from ground up. I like its MVC idea but I have rewritten most of its actions with JAX-RS resources. I will probably consolidate all the HTML and make it a single page application. The infrastructure will also be rewritten with vert.x to avoid dependency on application server. The UI will also be rewritten to with other framework, bootstrap, for example, but the whole theme setting will be kept still.

I hope it can share the same data with WP sooner. So I can blog with both software. And the themes too, I wish.
