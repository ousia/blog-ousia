---
tab: none
title: Touchpad Configuration
layout: page
permalink: /0001/
---

These are the contents to add in `/etc/X11/xorg.conf.d/30-touchpad.conf`:

```
Section "InputClass"
        Identifier "system-touchpad"
        Driver "libinput"
        MatchIsTouchpad "on"
        Option "Tapping" "on"
        Option "ScrollMethod" "edge"
        Option "HorizontalScrolling" "on"
EndSection
```
