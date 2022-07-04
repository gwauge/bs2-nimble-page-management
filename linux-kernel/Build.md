## Prerequisites

You need to intsall the following packages:
`sudo apt install make gcc libncurses-dev flex bison`

## Steps to build Kernel

- Copy the kernel `linux-5.6_rc6` to `home/$name/build`
- Go to kernel Directory `linux-5.6_rc6`
- Run `make mrproper`
- Then copy it to `usr/src` with `sudo cp -R linux-5.6_rc6 /usr/src/`
- Go to `usr/src/` and create a new kernel directory with `sudo mkdir linux-5.6`
- Now switch into it with `cd linux-5.6`
- And run `make O=/home/$name/build/linux-5.6_rc6 menuconfig`
- In the Kernel Menu go to `Memory Management` and make sure `NIMBLE_PAGE_MANAGEMENT` and `CONFIG_PAGE_MIGRATION_PROFILE` is activated. You can also search with `/` and then save the config
- Now build the Kernel with `make O=/home/$name/build/linux-5.6_rc6` and `sudo make O=/home/$name/build/linux-5.6_rc6 modules_install install`

## Compiling

- In order to boot your new kernel, you'll need to copy the kernel image (e.g. .../linux/arch/x86/boot/bzImage after compilation) to the place where your regular bootable kernel is found.

- Booting a kernel directly from a floppy without the assistance of a bootloader such as LILO, is no longer supported.

- If you boot Linux from the hard drive, chances are you use LILO, which uses the kernel image as specified in the file /etc/lilo.conf. The kernel image file is usually /vmlinuz, /boot/vmlinuz, /bzImage or /boot/bzImage. To use the new kernel, save a copy of the old image and copy the new image over the old one. Then, you MUST RERUN LILO to update the loading map! If you don't, you won't be able to boot the new kernel image.

- Reinstalling LILO is usually a matter of running /sbin/lilo. You may wish to edit /etc/lilo.conf to specify an entry for your old kernel image (say, /vmlinux.old) in case the new one does not work. See the LILO docs for more information.

- After reinstalling LILO, you should be all set. Shutdown the system, reboot, and enjoy!

- If you ever need to change the default root device, video mode, ramdisk size, etc. in the kernel image, use the rdev program (or alternatively the LILO boot options when appropriate). No need to recompile the kernel to change these parameters.

- Reboot with the new kernel and enjoy.
