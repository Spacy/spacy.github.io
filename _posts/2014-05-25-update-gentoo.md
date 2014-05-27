---
layout: post
title: 'Update gentoo system'
description: ''
category: '笔记'
tags: []
---

- Update repositories
```shell
emerge --sync
```

- Update *portage* if updated
```
emerge --oneshot portage
```

- Update *gcc* first. There might be some packages require to be compiled with the lastest gcc. See [gentoo wiki](http://wiki.gentoo.org/wiki/Upgrading_GCC)

- Update *world*
```
emerge -avuDN --with-bdeps y --keep-going --autounmask-write @world 
```

 + If there are slot conflicts, **unmerge** all the conflict packages.
**NOTICE**: This will unmerge some important packages. You must update @world immediately (before reboot).
```
emerge -C aaa bbb ccc
```

 + If there are Blocks, update the packages **oneshot**. (not tested)
```
emerge -1 aaa bbb ccc
```
Or mask the package in */etc/portage/package.mask*, or unmask package's highest version that is masked by *portage*
 
- Update configure files
```
etc-update
```

- Update kernel. See [Gentoo Kernel Upgrade Guide](https://negativesum.net/tech/linux/gentoo/kernel)

- Generate initramfs if you use firmwares or have seperate file system for /usr or /var. I use the option *--firmware*
```
genkernel --firmware
```
  Remember to update the grub configure file

- Reboot and remove the distfiles
```
eclean-dist
```



