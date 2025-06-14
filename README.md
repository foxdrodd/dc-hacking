# Dreamcast Hacking

Collection of some Dreamcast hacking information with other OSs like Linux, NetBSD.

Last tested Linux release on real hardware: **[dreamcast-linux 6.15.1](https://github.com/foxdrodd/dreamcast-linux)**

# Information sources

[Rich Knowledge Base of Dreamcast hacking](https://mc.pp.se/dc/sw.html)

Many great articles of technical details of the Dreamcast, like howto burn bootable CD-Rs, format of Bootloaders, System calls.

[Dreamcast Architecture | A Practical Analysis](https://classic.copetti.org/writings/consoles/dreamcast/)

[Dreamcast Wiki](https://dreamcast.wiki/Dreamcast.wiki)

[Dreamcast 32MB RAM upgrade](https://blog.ldtlb.com/2020/06/21/dreamcast-32mb-ram-upgrade.html)

"This article describes how to upgrade a Dreamcast from 16MB to 32MB of system SDRAM. I have done this exactly once, so this is still rather experimental. Please only attempt this with a spare Dreamcast you don’t mind destroying."

[Calibrate Laser of GDROM Drive](https://www.reddit.com/r/dreamcast/comments/45rto2/help_needed_measuring_potentiometer_resistance/)
/ [Laser Calibration](https://retro-hack.blogspot.com/2010/06/sega-dreamcast-laser-calibration-guide.html)

## YouTube

[X.org server on NetBSD/dreamcast 9.1](https://www.youtube.com/watch?v=ToVdC8B4waY&ab_channel=tsutsuii)

[NetBSD/dreamcast "root on GD-ROM" Boot CD Demonstration](https://www.youtube.com/watch?v=VJUbAvCg5NY&ab_channel=tsutsuii)

## github

[Slightly patched version of img4dc tools](https://github.com/Kazade/img4dc)

img4dc converts ISO files to CDI, that can be used on a gdemu

[KallistiOS](https://github.com/KallistiOS/KallistiOS)

Development environment and tools for homebrew dc

[Sega Dreamcast experiments](https://github.com/buhman/dreamcast)

Many code examples to be used with dc

## Linux on Dreamcast

[Dreamcast Linux Docker Build](https://github.com/foxdrodd/dreamcast-linux)

Builds Linux distro in docker container with current linux kernel.

[Dreamcast Linux, dusted off](https://github.com/classilla/dclinux)

Restored the historic linuxdc project from 2001, with components form the time.

[Dusting off Dreamcast Linux (Blog)](https://oldvcr.blogspot.com/2023/02/dusting-off-dreamcast-linux.html)

[Dreamcast Linux tools bootdreams (Forum Post)](https://www.dreamcast-talk.com/forum/viewtopic.php?t=15258)

[Working dreamcast-linux](http://www.lxdream.org/files/)

Old Files from 2001 that contain a working dreamcast-linux

[Dreamcast Linux Docker Build](https://github.com/andersevenrud/dreamcast-linux)

Nice Docker Container that cross-compiles a dreamcast linux kernel, uses sh-boot loader (currently, doesnt boot for me and needs some customization eg CONFIG_SH_DREAMCAST)

[Dusted-off Dreamcast Linux booting through GDEMU (YouTube)](https://www.youtube.com/watch?v=ygdGxo6wXM4)

## Emulators

[GXemul](https://gavare.se/gxemul/)

Dreamcast emulator, e.g. boot a ISO:

```
gxemul -XEdreamcast -dco23965696:data.raw 
```

# NetBSD

NetBSD officially supports Dreamcast and it really works, supports many features and peripherals.

[NetBSD on Dreamcast](https://wiki.netbsd.org/ports/dreamcast/)

[Booting NetBSD/dreamcast with GDEMU](https://mail-index.netbsd.org/port-dreamcast/2023/04/05/msg000323.html)

"I've successfully booted it on my Dreamcast with a GDEMU by taking the generated `data.raw` generated by `dc-burn-netbsd` and converting it to a cdi with cdi4dc (https://github.com/Kazade/img4dc)."



[Create Live CD](https://github.com/abs0/dc-burn-netbsd)

The creation of a Live-CD to boot on the Dreamcast works flawless.

From NetBSD, install `dc-tools` from pkgsrc.

Create Live-CD with base system, create data.raw to boot.

```
dc-burn-netbsd -s base -l
```

data.raw from the build-script:
```
gxemul -XEdreamcast -dco23965696:data.raw 
```

---
Burn Image as Multi-Session CD-R
see https://mc.pp.se/dc/cdr.html

```
dd if=/dev/zero bs=2352 count=300 of=audio.raw 
wodim dev=/dev/sr0 -v -multi -audio audio.raw
wodim dev=/dev/sr0 -v -multi -xa std-live.raw 
```

---

Alternatively, the data.raw from dc-burn-netbsd can be converted to cdi format and put on gdemu to boot. For this you need the tool cdi4dc from [img4dc](https://github.com/Kazade/img4dc).

```
cdi4dc data.raw output-for-gdemu.cdi
```
The resulting file can be put on gdemu and be booted.
