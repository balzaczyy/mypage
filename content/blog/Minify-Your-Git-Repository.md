---
title: Git版本库瘦身
date: '2013-11-11'
description:
categories:
- 技术

---

最近项目上进行了双线开发，为了给已经发布的信息中心打上最新的补丁，同时确保另一个基于相同代码线的项目能获得同样的补丁。我本地使用的是Git来管理不同分支的，由于一些历史原因，里面包含了些重量级的JDK和第三方库。为了适应双线开发，我不得不对我的Git版本库进行瘦身。

Stackoverflow上提供了很多讨论，基本的思路是使用filter-branch这条命令。由于讨论很零散，我主要遵循了[这篇博客的方法](http://naleid.com/blog/2012/01/17/finding-and-purging-big-files-from-git-history)。

首先获得所有文件的SHA键列表。

	git rev-list --objects --all | sort -k 2 > allfileshas.txt

整理Git版本库，并按照所占大小收集结果。

	git gc && git verify-pack -v .git/objects/pack/pack-*.idx | egrep "^\w+ blob\W+[0-9]+ [0-9]+ [0-9]+$" | sort -k 3 -n -r > bigobjects.txt

按照SHA查找文件的路径。

	for SHA in `cut -f 1 -d\  < bigobjects.txt`; do
		echo $(grep $SHA bigobjects.txt) $(grep $SHA allfileshas.txt) | awk '{print $1,$3,$7}' >> bigtosmall.txt
	done;

我的库包含100K个文件，显然是太慢了。于是写了一个Go脚本，稍显臃肿，但是很快。

<script src="https://gist.github.com/balzaczyy/7409628.js"></script>

然后把那些大的二进制文件一一干掉。这个过程很无聊，每个文件必须单独删除，然后clone，没有自动化。

	git filter-branch --prune-empty --index-filter 'git rm -rf --cached --ignore-unmatch MY-BIG-DIRECTORY-OR-FILE' --tag-name-filter cat -- --all
	git clone --no-hardlinks file:///Users/yourUser/your/full/repo/path repo-clone-name

结果令人满意，从原来的600MB减少到了现在的不到300MB。不过如果要完全替换远程版本库的话，还是比较麻烦，需要额外运行这个命令。

	git push --mirror

另外，如果遇到老的branch信息也被误保留的话（一般是不小心运行了pull和push命令），可以通过一个干净的新版本库来解决这个问题。