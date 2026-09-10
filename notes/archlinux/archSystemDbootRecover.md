# recovering from broken arch

1. `cfdisk` to drive
2. delete the boot partion and create a new EFI system
3. `mkfs.fat -F32 /dev/nvme0n1p1`

4. `mount /dev/nvme0n1p2 /mnt` or, `mount /dev/mapper/cryptroot /mnt`
5. `mount /dev/nvme0n1p3 /mnt/home` or `mount /dev/mapper/crypthome /mnt/home`
6. `mkdir -p /mnt/boot`
7. `mount /dev/nvme0n1p1 /mnt/boot`

8. `genfstab -U /mnt > /mnt/etc/fstab`
9. `arch-chroot /mnt`

10. `bootctl --path=/boot install`
11. reinstall the kernels, headers and drivers
12. edit /boot/loader/loader.conf
13. edit /boot/loader/entries/arch.conf
14. `exit`
15. `umount -a`
16. reboot

# recovering from broken cachyOS

1. `cfdisk` to drive
2. delete the boot partion and create a new EFI system
3. `mkfs.fat -F32 /dev/nvme0n1p1`

4. `mount /dev/nvme0n1p2 /mnt` or, `mount /dev/mapper/luks-UUID /mnt`
5. `mount /dev/nvme0n1p3 /mnt/home` or `mount /dev/mapper/luks-UUD /mnt/home`
6. `mkdir -p /mnt/boot`
7. `mount /dev/nvme0n1p1 /mnt/boot`

8. `genfstab -U /mnt > /mnt/etc/fstab`
9. `cachy-chroot /mnt`

10. `bootctl --path=/boot install`
11. reinstall the kernels, headers and drivers
12. `sdboot-manage gen` : this will automatically create entries
13. `exit`
14. `umount -a`
15. reboot

# recovering from broken endeavourOS

1. `cfdisk` to drive
2. delete the boot partion and create a new EFI system
3. `mkfs.fat -F32 /dev/nvme0n1p1`

4. `mount /dev/nvme0n1p2 /mnt` or, `mount /dev/mapper/luks-UUID /mnt`
5. `mount /dev/nvme0n1p3 /mnt/home` or `mount /dev/mapper/luks-UUD /mnt/home`
6. `mkdir -p /mnt/efi`
7. `mount /dev/nvme0n1p1 /mnt/efi`

8. `genfstab -U /mnt > /mnt/etc/fstab`
9. `arch-chroot /mnt`

10. `bootctl --path=/efi install`
11. run `reinstall-kernels` script
12. `exit`
13. `umount -a`
14. reboot
