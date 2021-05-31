# Installing Arch 🐧
  1. download ISO💿
  2. Flash ISO / add to VM
  3. boot

*** if on a VM, enable EFI boot***

```
  timedatectl set-ntp true
```

```
  fdisk -l
```
save path to main drive and run:
```
  fdisk /path/todrive
```
## Drive partitioning 🖴
```
  1. g
  2. n
  3. DEFAULT
  4. DEFAULT
  5. +550M
  6. n
  7. DEFAULT
  8. DEFAULT
  9. +2G
  10. n
  11. DEFAULT
  12. DEFAULT
  13. DEFAULT  
```
## Partition formating
### EFI
```
  1. t
  2. 1
  3. L (find code for EFI)
  4. q
  5. EFI code
```
### SWAP
```
  1. t
  2. 2
  3. L (find code for Linux swap)
  4. q
  5. swap code
```

```
  w
```
### Formating
```
  mkfs.fat -F32 /dev/sda1
  mkswap /dev/sda2
  mkfs.ext4 /dev/sda3(or another root partition)
  mount /dev/sda3 /mnt
  swapon /dev/sda2  
  mkdir -p /mnt/boot
  mount /dev/sda1 /mnt/boot
```

## Install 
### last of the more stressful steps 🎉
```
  pacstrap /mnt base linux linux-firmware
```
***this step will take some time 🕖***

## Configuration
```
  genfstab -U /mnt >> /mnt/etc/fstab
  arch-chroot /mnt
```
### Region config
#### find your region
```
  ls /usr/share/zoneinfo/ [TAB]
  ls /usr/share/zoneinfo/REGION/ [TAB]
```
you should now have a path: `usr/share/zoneinfo/REGION/CITY`
```
  ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
  hwclock --systohc
  pacman -S vim
```

### Locale config
Edit /etc/locale.gen and uncomment en_US.UTF-8 UTF-8
```
  vim /etc/locale.gen
  [UNCOMMENT YOUR LOCALE]
  locale-gen
```

### Hostname
```
  vim /etc/hostname
  [enter your desired hostname]
```

```
  vim /etc/hosts
```
Paste in the following (modify myhostname acordingly)
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	myhostname.localdomain	myhostname
```

```
  mkinitcpio -P
```

## Bootloader time 😨
### GRUB
```
  pacman -S grub efibootmgr
```

```
  grub-install --target=x86_64-efi --bootloader-id=GRUB --efi-directory=/boot --no-nvram --removable
  grub-mkconfig -o /boot/grub/grub.cfg
```
Change the root password:
```
  passwd
```

Restart
```
  exit
  umount -l /mnt
  reboot / shutdown now
```
