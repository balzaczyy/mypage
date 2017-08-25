---
title: tips: install scrollkeeper-0.3.14 @ cygwin
date: '2006-09-13'
---
I want to install gnome under cygwin environment, so I followed the BLFS 6.1 guide book. But cygwin doesn't provide scrollkeeper package and normal g-b-s method doesn't work, either. After a lot of Google, I turned to cygport, a building system for cygwin. But cygport is still under development and it doesn't provide the ebuild I need. I have to write it on my own. Here is my experiences:

1. Create scrollkeeper-0.3-14.cygport file in /usr/src.

		inherit gnome2
		DESCRIPTION="a cataloging system for documentation"
		SRC_URI="http://ftp.gnome.org/pub/GNOME/sources/scrollkeeper/0.3/scrollkeeper-0.3.14.tar.bz2"
		SRC_DIR="$PN-$PV.$PR"

2. Download the package manually in /usr/src.
The naming convention for package in cygport is strange, PACKAGENAME-VERSION-RELEASE. So here is the trick, turn 0.3.14 to 0.3-14. But you need to download the package manually.

3. Run 'cygport scrollkeeper-0.3-14 prep compile'.
Here is another trick. Usually the configuration would fail and result with some error msg like "run aclocal manually", "copy gettext.h" or "intl...". Please don't google the answer because it's useless. ***** When it pause, assume the build folder is "~/scrollkeeper-0.3-14", run 'touch ~/scrollkeeper-0.3-14/src/scrollkeeper-0.3.14/intl/Makefile.in". Continue the configuration and ignore all the warning message and ... everything is done.

4. Run 'cygport scrollkeeper-0.3-14 install finish'.
I'm not a package maintainer, so I don't test the above method on systems other than mine. Please refer to [http://cygwinports.dotsrc.org/](http://cygwinports.dotsrc.org/) for further good ebuild files.