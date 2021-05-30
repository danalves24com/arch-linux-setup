# Installing Arch 🐧
  1. download ISO💿
  2. Flash ISO / add to VM
  3. boot


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
  mkfs.ext4 /dev/sda3(or another root partition)
  mkswap /dev/sda2
  mount /dev/sda3 /mnt
  swapon /dev/sda2  
```

## Install 
### last of the more stressful steps 🎉
```
  pacstrap /mnt base linux linux-firmware
```
***this step will take some time 🕖***
