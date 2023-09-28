# HOW TO BUILD
1. Download OpenWRT source code **[openwrt-19.07.6](https://github.com/openwrt/openwrt/archive/v19.07.6.tar.gz)**
2. Download **[patch](https://github.com/lukaskronus/opi-r1-cyberwrt/raw/main/patch/All_openwrt-19.07.6-SPI-flash-firmware-16mb.patch)** to OpenWRT's folder
3. Apply the patch
```
patch -p1 < All_openwrt-19.07.6-SPI-flash-firmware-16mb.patch
```
4. Check if there is this line in *feeds.conf.default*

```
src-git opicyberwrt https://github.com/lukaskronus/opi-r1-cyberwrt.git
```
5. Update & Install packages
```
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
```
- Run "make menuconfig" to select your preferred configuration for the toolchain, target system & firmware packages. 
- Be sure to select web-cyberwrt and boot-config-mmc in utils.
```
make
```
- After compiled, flash the firmware to your board. Run the following command lines
```
cd /tmp
mtd -e uboot write sun8i-h2-plus_orangepi-r1-boot.bin uboot
mtd -e dtb write sun8i-h2-plus-orangepi-r1-dtb dtb
mtd -e firmware write sun8i-h2-plus-orangepi-r1-squashfs-sysupgrade.bin firmware
```
- When boot the first time, enter to boot configuration site
```
http://192.168.10.1/boot
```
**Note:** In order to working wireless, it requires to reboot again after configure your board.
