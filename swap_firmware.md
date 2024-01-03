# Swap firmware using Fastboot 

⚠️ **READ CAREFULLY!** ⚠️

The files you are downloading are not under my control. You accept the risk of using them. If your device or module were to break or even catch fire, I do not hold any responsibility in any way. Therefore, proceed at your own risk!

⚠️ Make sure to have a good backup of your QCN before proceeding! ⚠️

**Prerequisite**: Ensure that you have the adb and fastboot tools installed on your system. If you are using Windows OS, also download the `Google USB Drivers` from  [here](https://developer.android.com/studio/run/win-usb)

Download the desired software version, including a dummy QCN file and the `config` file, from this [MEGA folder](https://mega.nz/folder/KlhwlR5C#K0q2i7tdBYPFvdSESDUrPQ) 

## If you want to change firmware on your module (not hard-bricked) follow these steps:

- Enter module shell using `adb shell`
- Type the command `flash_erase /dev/mtd16 0 0` - this will erase the boot partition and force the module to boot directly into ***FASTBOOT Mode***
- Reboot it using command `reboot`

After a few seconds, it should appear as `Android ADB`. On Windows, it may not be recognized out of the box. Point to the folder where you extracted `Google USB Drivers` and select `Android Composite ADB Interface`.

Check if the device is recognized by running the command `fastboot devices`. If it is recognized, proceed.

Now navigate to the folder where you downloaded the firmware (use `CMD` prompt on Windows or Terminal on *\*NIX OS*) and run the following commands:

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

If everthing was fine, module should run with the new firmware

## Optional step, replace `config` file to match the firmware

After swapping the firmware, using `EFS Explorer`, replace the `config` file in the EFS root with the one corresponding to the firmware you are running. This will update the exposed version in `ATI` commands and, in some cases, enable RJ-11 ports on modules that support only `VoIP Mode`.
