---
title: PLUGINS_ROOT
date: '2012-09-24'
description:
categories:
- tech
tags:
---

PLUGINS_ROOT used by Eclipse help system to reference resources located in other plugins, which looks like "href='PLUGINS_ROOT/plugin_id/path/to/resource.html'". I can not really understand how it was created and I can not find any related mails or history discussions either.

Firstly, PLUGINS_ROOT is like a variable. But who would use a variable in an HTML page? We use variables in templates, like JSP, VM, PHP, etc. We don't use variables in HTML. Maybe we would in the future but not now. So it's ridiculous to put a lot of PLUGINS_ROOT in the HTML pages, just hope it got correctly resolved at run-time. Yes, that's why Eclipse help system support stand-alone mode, to allow us to verify it. Otherwise, you can not just open the browser to verify if the HTML renders correctly.

Secondly, PLUGINS_ROOT breaks link check tool. Right, just check my hundreds of warnings in the Eclipse workspace, just because Eclipse doesn't recognized PLUGINGS_ROOT. It's unacceptable for people like us, who prefer a cleaner workspace without any IDE warnings.

Finally, PLUGINS_ROOT sounds like a hack. As far as I know, there is no such scenario that can not be supported with relative links. And it won't save a lot of effort to use PLUGINS_ROOT than calculating the number of "../" typing required. However, we still have to support it for the sake of existing legacy content and their maintainers.

I can't understand its value but I hope it's not used any more.
