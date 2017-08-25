---
title: 试用LedisDB
date: '2014-08-15'
description:
categories:

tags:

---

最初是从InfoQ上得知[LedisDB](http://ledisdb.com)这个项目的，号称[“Go编写的高性能NoSQL数据库”](http://www.infoq.com/cn/news/2014/08/cloud-structure-thinking)，其实最吸引我的还是其能够嵌入在Go应用中使用。LedisDB有一套自己的构建方法，不过因为我不需要它独立运行，所以走了一条捷径。整个过程并不是一帆风顺，不过也没遇到很大的困难。

要在Go写的应用中使用LedisDB，首先要下载它的源代码和依赖项目的代码：

	go get github.com/ledisdb
	go get github.com/siddontang/go-log/log
	go get github.com/siddontang/go-snappy/snappy
	go get github.com/siddontang/goleveldb/leveldb
	go get github.com/szferi/gomdb

如果是Windows系统的话，需要安装[MinGW-w64](http://sourceforge.net/projects/mingw-w64/)来构建最后的LMDB。不过即使编译通过也是不能运行的，会遇到

	undefined: strdup

经过Google发现strdup是个非标准函数，可以找到标准实现。我后来问了LedisDB的作者，发现LMDB在Windows上也是不能用的，所以就没有深入下去尝试。同时，我发现LedisDB的对于后台数据引擎的管理，是采用集中式的方法，也就是在store的包里面统一注册，没有办法单独跳过。LedisDB自带的构建脚本能够根据所在的操作系统，自动跳过某些源代码，所以没有这个问题。因为我是直接嵌入使用，没有经过一个构建过程，所以只能手动删除相应的mdb.go文件即可。

除此之外，如果把mdb注册的方法移到mdb这个具体的包里面也是可以，不过这可能并不符合LedisDB原先的设计和现有的构建脚本。

我主要使用LedisDB作为一个可持久化的缓存，因为Bluemix每个实例的硬盘和内存大小是1G，而且实例自动迁移的时候可能会造成硬盘数据丢失，所以LedisDB用在这里不会显得浪费，数据丢失的成本也不太大，今后可以加上主动式数据更新以及双实例热备，那基本就满足要求了。

要初始化一个简单的LedisDB对象还蛮简单的：

	var cache *ledis.DB
	var err error
	if cache, err = func() (*ledis.DB, error) {
		cfg := config.NewConfigDefault()
		l, err := ledis.Open(cfg)
		if err != nil {
			return nil, err
		}
		return l.Select(0)
	}(); err != nil {
		log.Fatal(err)
	}

我目前基本上只会用到Get和Set方法，将来可能会用到expire之类的，控制内存的使用。

	var data []byte
	if data, err = cache.Get([]byte(file)); err != nil {
		log.Printf("Error reading cache: %v", err)
	}
	if len(data) == 0 {
		// ... obtain data from remote service

		if err = cache.Set([]byte(file), data); err != nil {
			log.Printf("Error writing cache: %v", err)
		}
	}

我已经在这里使用了LedisDB，内存占用很小，很符合Go应用小而易用的特点，Good！