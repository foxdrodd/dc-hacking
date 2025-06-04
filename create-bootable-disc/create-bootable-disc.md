# Create bootable disc

![Disc structure](dreamcast.drawio.svg)

## Tools

Needs: [scramble](https://github.com/KallistiOS/KallistiOS/tree/master/utils/scramble), mkisofs, [makeip](https://github.com/KallistiOS/KallistiOS/tree/master/utils/makeip) (or existing IP.BIN), [img4dc](https://github.com/Kazade/img4dc)

## Creation

1. Get or create a IP.BIN (contains the name of 1ST_READ.BIN), read 1)
2. scramble 1ST_READ.BIN, read 1) get tools from 3)
3. mkisofs -C 0,11702 -V imgname -G IP.BIN -l -o temp.iso 1ST_READ.BIN
4. cdi4dc temp.iso temp.cdi
5. Copy temp.cdi to gdemu or use temp.iso in gxemul


## Sources
1. [Structure of IP.BIN and 1ST_READ.BIN](https://mc.pp.se/dc/ip.bin.html)
2. [Structure of bootable CD-Rs](https://mc.pp.se/dc/cdr.html)
3. [KallistiOS Utils](https://github.com/KallistiOS/KallistiOS/tree/master/utils)