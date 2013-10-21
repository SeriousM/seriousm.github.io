---
layout: post
title:  "Determine ClickOnce UpdateUri / Install Address"
date:   2011-04-06 13:02:00
categories: Work DotNet
---

Its hard to find Informations about the place where the UpdateUri is saved on a windows machine.
The only information i was found is where the binaries of a ClickOnce application is stored.

This whould be:
`C:\Users\UserName\AppData\Local\Apps\2.0\` (Vista)
`C:\Documents and Settings\UserName\Local Settings\Apps\2.0\` (XP)

The UpdateUri of a particular application can be found in the registry:

`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Uninstall\[APP-ID]\UrlUpdateInfo`

The key will contain a string like this:
http://somedomain.com/ApplicationName/ApplicationName.application

If this address is called in the browser (InternetExplorer or Firefox with AddOn), the application starts to install.

If you change the `ApplicationName.application` to `publish.htm`, a install page will be displayed.