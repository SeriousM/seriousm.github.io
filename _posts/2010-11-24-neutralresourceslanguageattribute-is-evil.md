---
layout: post
title:  "NeutralResourcesLanguageAttribute is Evil for ResourceFiles"
date:   2010-11-24 14:08:00
categories: Projects WPFLocalizeExtension
---

Imagine this:
Two Resource files named `Strings.resx` and `Strings.de.resx`.
The first (neutral) contains english content, the second german content.

If you ask youself over and over again why the f**k the ResourceManager returns the neutral language even you use the specified language `de`, look into your AssemblyInfo.cs file.

If there is a `[assembly: NeutralResourcesLanguage("de")]`, the ResourceManager from this Assembly thinks you want to get the neutral language if you ask for `de` explicit.

This attribute is used to overrule the neutral settings to a specific one.

Deleting this from your `AssemblyInfo.cs` can help you realy much in this case.