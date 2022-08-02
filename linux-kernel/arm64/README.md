# Linux kernel 5.6.0-rc6 for arm64

## Prerequisites

Have an arm64 machine ready with a suited linux distribution installed (e.g. ubuntu).
You need to install the following packages:
`sudo apt install make gcc-8 libncurses-dev flex bison libssl-dev`
Select gcc-8 via `sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 8` command
And download the kernel file here: [linux-5.6_rc6.zip](https://drive.google.com/file/d/1hhbfEWTdk0hkAeEN3y7M32KZ-7t9bPR_/view?usp=sharing)

## Steps to build Kernel

- Copy the kernel `linux-5.6_rc6` to `home/$name/build`
- Go to kernel Directory `linux-5.6_rc6`
- Run `make mrproper`
- And run `make menuconfig`
- In the Kernel Menu go to `Memory Management` and make sure `NIMBLE_PAGE_MANAGEMENT` is activated. You can also search with `/` and then save the config
- In the created config file `.config` edit it and search for `CONFIG_SYSTEM_TRUSTED_KEYS` and this must be an empty string like this `CONFIG_SYSTEM_TRUSTED_KEYS=""` as well as `CONFIG_DEBUG_INFO_BTF` must be disabled, so it looks like this `CONFIG_DEBUG_INFO_BTF=n`
- Apply this [Patch](https://github.com/torvalds/linux/commit/53fa117bb33c9ebc4c0746b3830e273f5e9b97b7) to the respective files
- The -j option is used to assign more cores to the process so that the process speeds up. To know the number of cores available, use the `nproc` command.
- Now build the Kernel with `make -j <corenumber>`
- Finally run `sudo make modules_install install` and `sudo make install`

## Enable kernel for boot

- Run `sudo update-initramfs -c -k 5.6.0-rc6`
- If you want to select the kernel via _grub_ and press `shift` while booting to select folow these steps:

  - Go to `etc/default` and edit your grub file with `sudo gedit grub` and change the according lines to this:

  ```bash
  GRUB_TIMEOUT_STYLE=menu
  GRUB_TIMEOUT=#
  ```

  and run `sudo update-grub`

- After this reboot your system with the `reboot` command
- select compiled kernel after booting and check with `uname -mrs`
