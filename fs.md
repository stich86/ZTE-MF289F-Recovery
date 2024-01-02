# Partition Layout & Filesystem Information

Here is the partition layout together with filesystem information about MF289F module:

| Dev    | Size     | Erase Size | Name          |
|--------|----------|------------|---------------|
| mtd0   | 00280000 | 00040000   | "sbl"         |
| mtd1   | 00280000 | 00040000   | "mibib"       |
| mtd2   | 00b00000 | 00040000   | "efs2"        |
| mtd3   | 00600000 | 00040000   | "efs2bak"     |
| mtd4   | 001c0000 | 00040000   | "tz"          |
| mtd5   | 00100000 | 00040000   | "tz_devcfg"   |
| mtd6   | 00180000 | 00040000   | "ddr"         |
| mtd7   | 00100000 | 00040000   | "apdp"        |
| mtd8   | 00100000 | 00040000   | "xbl_config"  |
| mtd9   | 00100000 | 00040000   | "multi_image" |
| mtd10  | 00100000 | 00040000   | "aop"         |
| mtd11  | 00100000 | 00040000   | "qhee"        |
| mtd12  | 00100000 | 00040000   | "abl"         |
| mtd13  | 00280000 | 00040000   | "uefi"        |
| mtd14  | 00180000 | 00040000   | "toolsfv"     |
| mtd15  | 00180000 | 00040000   | "loader_sti"  |
| mtd16  | 00b40000 | 00040000   | "boot"        |
| mtd17  | 00100000 | 00040000   | "scrub"       |
| mtd18  | 04b40000 | 00040000   | "modem"       |
| mtd19  | 001c0000 | 00040000   | "misc"        |
| mtd20  | 00180000 | 00040000   | "devinfo"     |
| mtd21  | 00d00000 | 00040000   | "recovery"    |
| mtd22  | 001c0000 | 00040000   | "fota"        |
| mtd23  | 03000000 | 00040000   | "recoveryfs"  |
| mtd24  | 00100000 | 00040000   | "sec"         |
| mtd25  | 00a00000 | 00040000   | "ztefile"     |
| mtd26  | 09600000 | 00040000   | "zterw"       |
| mtd27  | 0a1c0000 | 00040000   | "system"      |


The most important partitions that usually need to be swapped between different firmwares are: ***efs2, uefi, modem, boot and system***:

| Partition Name | Description                                                                                                                                                                                                             |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **efs2**       | Contains all baseband configuration (IMEI, BB settings and so on). Be careful and make a backup of the whole partition using Qualcomm Tool (QPST to backup as QCN file).                                                |
| **uefi**       | Contains the [RexOS](https://en.wikipedia.org/wiki/REX_OS) system that is loaded by the baseband. It will read all DSP firmwares from the modem partition (AKA NON-HLOS) to initialize all radio stuff.                 |
| **modem**      | Contains all DSP firmwares loaded by UEFI.                                                                                                                                                                              |
| **boot**       | It's the Linux Kernel used by the AP processor to load embedded drivers and start everything from Root FS                                                                                                               |
| **zterw**      | It's used by Root FS to store all settings that should be persistent across reboots. When you factory reset the module, by using either the physical or WebUI button, the volumes inside this ***UBI*** will be formatted. |
| **system**     | It's the Linux Root FS where all binaries are stored and ran at boot after kernel startup.                                                                                                                              |

**system** & **modem** partitions are created using ***UBIFS*** on top of an ***UBI*** image layout. Both can be accessed in read-write using ADB, so changes on the filesystem are possible.

**system** contains 2 volumes:

| Volume Name | Description                                                                                              |
|-------------|----------------------------------------------------------------------------------------------------------|
| ***rootfs***      | Contains all Linux and ZTE executables, it can modified to add sshd/telnetd and other tools        |
| ***zte_data***    | Contains EFS default configuration used after the device has been reset; default AND custom parameters used by ZTE binaries, like enabled bands or APNs |

These two volumes can be extracted using [ubireader](https://github.com/onekey-sec/ubi_reader).

If you want to dig on it, please refer to [my ZTE MC7010 istruction](https://github.com/stich86/ZTE-MC7010/blob/main/fs.md) on how to repack sysfs 
