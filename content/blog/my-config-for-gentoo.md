---
title: My make.conf for Gentoo
date: '2005-10-31'
description:
categories:
- tech
---
	# These settings were set by the catalyst build script that automatically
	built this stage
	# Please consult /etc/make.conf.example for a more detailed example
	CFLAGS="-pipe -O3 -march=pentium4"
	CHOST="i686-pc-linux-gnu"
	CXXFLAGS="${CFLAGS}"
	LDFLAGS="-Wl,-O1"
	MAKEOPTS="-j4"
	USE="a52 aac acpi bash-completion bzip2 cdparanoia cdr cjk dbus dga
	divx4linux dvd exif fbcon ffmpeg flac ftp glut gtkhtml hal imlib2
	immqt-bc javascript joystick kdeenablefinal kerberos kqemu matroska
	mmx mmxext moznocompose moznoirc moznomail mozsvg mplayer msn nptl
	nptlonly nvidia openal pic rdesktop sharedmem sse sse2 svg swat
	theora threads unicode v4l v4l2 vcd vim-with-x win32codecs xosd xpm
	xvid zeroconf -gnome"
	LINGUAS="en zh_CN"
	FEATURES="ccache distcc"
	CCACHE_SIZE="2G"
	#CCACHE_DIR="/var/tmp/ccache"
	DISTCC_DIR="/var/tmp/portage/.distcc"
	#DISTCC_HOSTS="gentoo-bc gentoo-home"
	
	GENTOO_MIRRORS="http://mirror.gentoo.gr.jp http://gentoo.gg3.net/
	http://ftp.gentoo.or.kr/ http://gentoo.channelx.biz/ http://gentoo.kems.net"