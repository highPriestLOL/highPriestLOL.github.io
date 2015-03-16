---
layout: post
title: Meet Pacgraph
category: Arch Linux
tags:
- Arch Linux
- pacgraph
- linux
- pacman
---

Pacgraph is a tool on Arch linux to graphically represent all your installed packages.

```BASH
pacman -S pacgraph
```

By default, pacgraph generates an SVG and PNG of all your packages and their dependencies. You can customize the output though. The svg below was generate by.

```BASH
pacgraph -b "#302e23" -l "#94c52a" -t "#b5c94a" -d "#cbee98"
```

![_config.yml]({{ site.baseurl }}/images/pacgraph.png)

For more [pacgraph options](http://kmkeen.com/pacgraph/index.html).
