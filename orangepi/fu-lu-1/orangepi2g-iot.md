来源于[https://en.opensuse.org/HCL:Orange\_Pi\_2G-IoT](https://en.opensuse.org/HCL:Orange_Pi_2G-IoT)

HCL:Orange Pi 2G-IoT

The Xunlong Orange Pi 2G-IoT is a single-board computer.

Contents

```
1 Technical data
2 Manual installation
2.1 U-Boot
2.2 Kernel
3 See also
```

Technical data

```
RDA 8810PL SoC
1x ARM Cortex-A5 CPU
256 MB RAM
40-pin connector
Manual installation
```

The baudrate of the debug UART is 921600. You may need to use a tool such as minicom or picocom rather than screen.

U-Boot

Mainline U-Boot does not yet contain support for this board or SoC.

```
git clone 
https://github.com/RDA8810/u-boot-RDA8810.git

make rda8810_config
make
```

You may want to tweak include/configs/rda\_config\_defaults.h.

```
dd if=u-boot.rda of=/dev/sdX bs=512 seek=256 iflag=fullblock oflag=direct
```

#### Kernel

The 4.12 kernel does not contain support for this board and SoC.

An initial [patchset](http://lists.infradead.org/pipermail/linux-arm-kernel/2017-June/515951.html) was submitted for 4.14. v1

For the vendor U-Boot you will need to append the .dtb:

```
cat arch/arm/boot/zImage arch/arm/boot/dts/rda8810pl-orangepi-2g-iot.dtb > zImage+dtb
```

From the U-Boot prompt, boot similar to this:

```
mux_config
setenv bootargs 'earlycon'
fatload mmc 0:1 ${kernel_addr} zImage+dtb
fatload mmc 0:1 ${script_addr} rda8810pl-orangepi-2g-iot.dtb
bootz ${kernel_addr} - ${script_addr}
```



