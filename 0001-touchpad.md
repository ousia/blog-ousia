---
tab: none
title: Touchpad Configuration
layout: page
permalink: /0001/
---

These are the contents to add in `/etc/X11/xorg.conf.d/30-touchpad.conf` (especially if you use _Fedora_[^fedora]):

[^fedora]: It is only a _Linux_ distribution, I know. But I don’t know whether other distributions may have a different path for these files (in any case, under the `/etc` directory).

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

### Notes
