---
title: Lucene和RMI
date: '2012-09-22'
description:
categories:
- 技术
tags:
- lucene
---

<p style="color: #000000; font-family: 'Lucida Grande';">从MarsEdit的角落里找到了这篇自己写的，但是没有发表的日志。稍加修改后，备份在这里。另外，日志里提到的<a href="http://book.douban.com/subject/3726306/">Lucene in Actions</a>的确是用搜索引擎必看的书。</p>
<p style="color: #000000; font-family: 'Lucida Grande';">I have been using Lucene for nearly three years. With self-google and various Java info sites' help, I created a Lucene based search engine piece by piece, to allow incremental index build, concurrent index sessions, multiple index reuse and management, and various performance tweaks. But seriously, I haven't finished any Lucene related book yet. And I'm reading one now, <em>Lucene in Actions</em>.</p>
<p style="color: #000000; font-family: 'Lucida Grande';">It's Chapter 6 now, and apparently I didn't use any filter to obtain the performance gain through filter reuse. I'm going to do that in a separate branch, and enhance the current caches, including</p>
<ul style="color: #000000; font-family: 'Lucida Grande';">
<li>filter cache</li>
<li>field cache</li>
<li>result cache</li>
</ul>
<p style="color: #000000; font-family: 'Lucida Grande';">I'm also going to try RMI method to do distributed Lucene search, and do a comparison together with my original JGroups method. Hope it's better because I don't really want to ship JGroups method due to its unfriendly license.</p>
