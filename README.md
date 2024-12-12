# lsblk
     ___     ___   ___ __       _ _ _____
     \  \  __\__\__\  \  \  __ / / /     \
      \  \/  __/    \  \  \/ // / /   .   \
       \  \___ \  \  \  \_   \\ \ \    \  /
        \___\__/\____/\___\/\_\\_\_\____\/

List information about block devices in the FreeBSD system.

I often need(ed) to work with Linux systems - and there is `lsblk(8)` command.

Anything closest to it (but still far away) in FreeBSD land are:

```
# geom disk list
# camcontrol devlist
# gpart show
# mount
# zfs list
```

... and none of these tools provide complete information like `lsblk(8)` does.

So I wrote `lsblk(8)` in POSIX `/bin/sh` for FreeBSD.

It only supports two modes.

The default one w/o any arguments.

Listing entire disks with `-d` option.

Hope that helps.

Below you will see examples of **lsblk(8)** usage.

![lsblk(8) Examples](https://github.com/vermaden/lsblk/raw/master/lsblk.examples.png)



