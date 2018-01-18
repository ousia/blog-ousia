---
tab: none
title: RPM List of Installed Packages
layout: page
permalink: /0002/
---

I use _Fedora_ on my main computer---which is a latop. When a new version is released, I install it from scratch.

Since I want to install all the packages that I had in the previous version, I need a complete list to install these with the newer version.

The easiest way to get a complete list of installed packages is:

```
rpm -qa
```

This will list all installed packages. To get the alphabetically--ordered list in a file (such as `fedora-27-packages.txt`[^namesample]):

[^namesample]: Of course, it is only an example. You may use any other file name. Either it doesn’t contain blank spaces, or you have to enclose the name in quotation marks.

```
rpm -qa | sort > fedora-27-packages.txt
```

The previous file containing the list of installed packages would be useful to manually check what is missing from your installed packages. All packages are listed with their version number.

If you want to install all packages automatically (using `dnf install`), you need to have only the package names. The way to do it:

```
rpm -qa --qf "%{NAME}\n" | sort > fedora-27-packages.txt
```

### Notes
