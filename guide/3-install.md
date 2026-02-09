<img align="right" src="https://github.com/n00b69/woa-cepheus/blob/main/cepheus.png" width="350" alt="Windows 11 running on a Xiaomi Mi 9">

# Running Windows on the Xiaomi Mi 9

## Installing Windows

### Prerequisites
- [tools（include BCD，bcdboot，ntfs-3g and so on）](https://www.123912.com/s/P6j5Vv-encKv) (should already be installed)

- [Windows on ARM image（have drivers）](https://www.123912.com/s/lGrLjv-hgFk)

- [UEFI](https://github.com/qaz6750/XiaoMi9-Drivers/releases/latest) (make sure you select MuCepheusDisableSecureBoot.img)

### Install termux


### Installing Windows
> [!Important]
> Do not install, or update to, Windows 11 25H2 26200.7XXX or higher! You will not be able to boot into this build due to a BSoD issue!

> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named win.wim or 22631.2861.XXXXXXX.esd)

```cmd
mkdir /mnt/win
mkdir /mnt/esp
mount /dev/block/your ESP partition /mnt/esp
path/to/ntfs-3g /dev/block/your Windows partition /mnt/win
path/to/wimlib-imagex apply /path/to/win.wim 2 /mnt/win     --no-acls     --no-attributes
```


### Copying your boot.img into Windows
- Drag and drop the **rooted_boot.img** from the **platform-tools** folder into the **WINCEPHEUS** disk in Windows Explorer, then rename it to **boot.img**.

#### Create Windows bootloader files

```cmd
cp /mnt/win/Windows/Boot/EFI/Microsoft/Boot/* /mnt/esp/EFI/Microsoft/Boot
cp path/to/your BCD  /mnt/esp/EFI/Microsoft/Boot
path/to/bcdboot /mnt/esp/EFI/Microsoft/Boot/BCD /dev/block/your Windows partition
```




#### Boot into the UEFI
> Replace `path\to\cepheus-uefi.img` with the actual path of the UEFI image
```cmd
fastboot boot path\to\cepheus-uefi.img
```

### Reboot to Android
Your device should reboot by itself after +- 10 minutes of waiting, after which you will be booted into Android, for the last step.

## [Last step: Setting up dualboot](/guide/dualboot-selection.md)




















