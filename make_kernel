#!/bin/sh

MAKEOPTS='-j5'

kernel=$(readlink -f /usr/src/linux | cut -c 16-)
cd /usr/src/linux

make_kern() {
  make $MAKEOPTS &&
  emerge -1 @module-rebuild
}

make_copy() {
  cp arch/x86_64/boot/bzImage /boot/vmlinuz-$kernel &&
  make modules_install &&
  dracut -H '' $kernel --force &&
  cp -v /boot/initramfs-$kernel.img /boot/EFI/gentoo/initrd.img && 
  cp -v /boot/vmlinuz-$kernel /boot/EFI/gentoo/kernel.efi
}

make_kern &&
make_copy ||
echo Failure >&2
