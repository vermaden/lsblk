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

For comparison - this is how Linux version of `lsblk(8)` output looks like.

```
[root@rhidm ~]# lsblk
NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
vda           252:0    0   20G  0 disk
├─vda1        252:1    0  600M  0 part /boot/efi
├─vda2        252:2    0    1G  0 part /boot
└─vda3        252:3    0 18.4G  0 part
  ├─rhel-root 253:0    0 16.4G  0 lvm  /
  └─rhel-swap 253:1    0    2G  0 lvm  [SWAP]

[root@rhidm ~]# lsblk -d
NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
vda  252:0    0  20G  0 disk

```

... and mine `lsblk(8)` on FreeBSD system.

```
FreeBSD # lsblk
DEVICE         MAJ:MIN SIZE TYPE                                    LABEL MOUNT
ada0             0:123 489G GPT                                         - -
  ada0p1         0:128 260M efi                              gpt/efiboot0 /boot/efi
  ada0p2         0:129 512K freebsd-boot                     gpt/gptboot0 -
  <FREE>         -:-   492K -                                           - -
  ada0p3         0:130 4.0G freebsd-swap                 gpt/freebsd-swap SWAP
  ada0p4         0:131 485G freebsd-zfs                   gpt/freebsd-zfs <ZFS>
  <FREE>         -:-   500K -                                           - -
nda0             0:107 477G GPT                                         - -
  <FREE>         -:-   1.0M -                                           - -
  nda0p1         0:109 100M efi                                   gpt/EFI -
  nda0p2         0:111  16M ms-reserved                   gpt/MS/reserved -
  nda0p3         0:113 476G ms-basic-data               gpt/MS/data/basic -
  <FREE>         -:-   698K -                                           - -
  nda0p4         0:115 509M ms-recovery                   gpt/ms-recovery -
  <FREE>         -:-   1.3M -                                           - -

FreeBSD # lsblk -d
DEVICE SIZE MODEL
ada0   489G Crucial CT525MX300SSD1
nda0   477G INTEL SSDPEKNW512GZL
-      966G TOTAL SYSTEM STORAGE

```
