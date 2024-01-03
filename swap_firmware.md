# Swap firmware using Fastboot 

⚠️ READ CAREFULLY! ⚠️
The files you are downloading are not under my control. You accept the risk of using them. If your device or module were to break or even catch fire, I do not hold any responsibility in any way. Therefore, proceed at your own risk!

⚠️ Be sure to have a good backup of your QCN before go ahead! ⚠️

Prerequisite: have `adb` and `fastboot` tools installed on your system. If you are running Windows OS, please download also `Google USB Drivers` from [here]https://developer.android.com/studio/run/win-usb
Download software version (with also dummy QCN file and `config` file) you want to run this [MEGA folder](https://mega.nz/folder/KlhwlR5C#K0q2i7tdBYPFvdSESDUrPQ) 

If you want to change firmware on your module (that is not hard-bricked) you can just follow these steps:

- Enter module shell using `adb shell`
- Type command `flash_erase /dev/mtd16 0 0` - this will erase boot partition and make the module to boot directly in ***FASTBOOT Mode***
- Reboot it using command `reboot`

After few seconds, it should be pop-up as "Android ADB". On Windows it cannot be recogniezed, just point to the folder where you have extracted `Google USB Drivers` and select `Android Composite ADB Interface`

Just check if you can see device running command `fastboot devices`. If there is one you can go ahead.

Now proceed on the folder where you have the downloaded firmware (using `CMD` prompt on Windows or Termina on *\*NIX* OS) and run these commands:

## Erase partitions

```
fastboot erase ZTERW
fastboot erase uefi
fastboot erase system
fastboot erase modem
```

## Write new firmware

```
fastboot flash uefi uefi.elf
fastboot flash modem NON-HLOS.ubi
fastboot flash boot sdxpoorwills-boot.img  
fastboot flash system sdxpoorwills-sysfs.ubi 
```

## Reboot module
`fastboot reboot`

If everthing was fine, module should run with new firmware

## Optional step, replace `config` file to match its firmware

After you have swapped the firmware, using `EFS Explorer`, just replace `config` file into EFS root with the one of the firmware you are running. This will replace exposed version on `ATI` commands, and in case enable RJ-11 ports on module that support only in `VoIP` Mode