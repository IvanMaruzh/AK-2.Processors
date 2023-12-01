## Computer architecture 2. Processors. Laboratory work № 4.
Laboratory work № 4.

Group: IO-13

Student: Ivan Maruzhenko

# Setup

```
export PATH=/opt/gcc-arm-8.3-2019.03-x86_64-arm-linux-gnueabihf/bin:$PATH
```
```
export CROSS_COMPILE="ccache arm-linux-gnueabihf-"
```
```
export ARCH=arm
```
```
export KDIR=$HOME/repos/linux-stable
```
# Compile

```
make clean
```
```
make
```
```
cp hello1.ko $HOME/repos/busybox/_install/
```
```
cp hello2.ko $HOME/repos/busybox/_install/
```
```
cp -r inc/ $HOME/repos/busybox/_install/
```
# Rebuild

Commands for rebuild archive:
```
cd ~/repos/busybox/_install
```
```
find . | cpio -o -H newc | gzip > ../rootfs.cpio.gz
```
```
cd ..
```
# Start QEMU

```
qemu-system-arm -kernel _install/boot/zImage -initrd rootfs.cpio.gz -machine virt -nographic -m 512 --append "root=/dev/ram0 rw console=ttyAMA0,115200 mem=512M"
```
# Kernel commands

```
modinfo hello1.ko
```
```
modinfo hello2.ko
```
```
insmod hello1.ko
```
```
insmod hello2.ko
```
```
rmmod hello2.ko
```
```
rmmod hello1.ko
```

# Debug commands
```
cat /sys/module/hello2/parameters/val
```
```
cat /proc/kallsyms | grep "print_hello"
```
