# Steps to put module in EDL Mode (on Linux) and play with partitions

Before starting, be sure you have [Bjoern Kerler's EDL tools](https://github.com/bkerler/edl) and sg3-utils already installed on your machine.

Please use this [prog_firehose.mbn](https://mega.nz/file/6g5nQSDD#mr1E2x2sG2sMmNuRYVa1kisY6ZQ1XYG-xKSpwgBHHkg) as loader to interact with the module.

⚠️ All commands must be run as ***root*** to avoid any issues with permissions ⚠️

Connect the module to your PC using a mPCIe-to-USB adapter, when you can see the module with the command `adb devices`:

```
List of devices attached
P685M135MZTED000000	device
```

Then type `adb reboot edl` to put it in ***EDL mode***

Use `lsusb` to check the following entry is available:

```
lsusb | grep 9008
Bus 004 Device 032: ID 05c6:9008 Qualcomm, Inc. Gobi Wireless Modem (QDL mode)
```

If everything worked, the module is now in ***EDL mode*** :-)

# Let's play with the edl tools

With the module in ***EDL mode***, edl commands can be used to check, dump, erase or write partitions.

Run this command to show the current layout of the firmware's partitions:

`edl printgpt --memory=NAND --loader=/path/to/prog_firehose.mbn`

Output example:

```
Qualcomm Sahara / Firehose Client V3.61 (c) B.Kerler 2018-2023.
main - Using loader prog_firehose_mf289f.mbn ...
main - Waiting for the device
main - Device detected :)
sahara - Protocol version: 2, Version supported: 1
main - Mode detected: sahara
sahara -
------------------------
HWID:              0x000960e100000000 (MSM_ID:0x000960e1,OEM_ID:0x0000,MODEL_ID:0x0000)
CPU detected:      "SDX24"
PK_HASH:           0xd4xxxxxxxxx
Serial:            0x0xxxxxxxxxx

sahara - Protocol version: 2, Version supported: 1
sahara - Uploading loader prog_firehose_mf289f.mbn ...
sahara - 32-Bit mode detected.
sahara - Firehose mode detected, uploading...
sahara - Loader successfully uploaded.
main - Trying to connect to firehose loader ...
firehose_client
firehose_client - [LIB]: No --memory option set, we assume "eMMC" as default ..., if it fails, try using "--memory" with "UFS","NAND" or "spinor" instead !
firehose
firehose - [LIB]: Couldn't detect MaxPayloadSizeFromTargetinBytes
firehose
firehose - [LIB]: Couldn't detect TargetName
firehose - TargetName=Unknown
firehose - MemoryName=eMMC
firehose - Version=1
firehose - Trying to read first storage sector...
firehose - Running configure...
firehose
firehose - [LIB]: Memory type eMMC doesn't seem to match (Failed to init). Trying to use NAND instead.
firehose
firehose - [LIB]: Couldn't detect MaxPayloadSizeFromTargetinBytes
firehose
firehose - [LIB]: Couldn't detect TargetName
firehose - TargetName=Unknown
firehose - MemoryName=nand
firehose - Version=1
firehose - Trying to read first storage sector...
firehose - Running configure...
firehose
firehose - [LIB]: Couldn't detect MaxPayloadSizeFromTargetinBytes
firehose
firehose - [LIB]: Couldn't detect TargetName
firehose - TargetName=Unknown
firehose - MemoryName=nand
firehose - Version=1
firehose - Trying to read first storage sector...
firehose - Running configure...
firehose - Storage report:
firehose - total_blocks:2048
firehose - block_size:262144
firehose - page_size:4096
firehose - num_physical:1
firehose - manufacturer_id:44
firehose - serial_num:0
firehose - fw_version:
firehose - mem_type:NAND
firehose - prod_name:
firehose_client - Supported functions:
-----------------
firehose - Nand storage detected.
firehose - Scanning for partition table ...
Progress: |██████████| 100.0% Scanning (Sector 0x400 of 0x400, ) 0.00 MB/s
firehose - Found partition table at sector 640 :)
oneplus
oneplus - [LIB]: No module named 'qrcode'
firehose - Nand storage detected.
firehose - Scanning for partition table ...

Parsing Lun 0:
Name                Offset		Length		Attr			Flash
-------------------------------------------------------------
sbl             	00000000	00280000	0xff/0x1/0x0	0
mibib           	00280000	00280000	0xff/0x1/0xff	0
efs2            	00500000	00B00000	0xff/0x1/0xff	0
efs2bak         	01000000	00600000	0xff/0x1/0xff	0
tz              	01600000	001C0000	0xff/0x1/0x0	0
tz_devcfg       	017C0000	00100000	0xff/0x1/0x0	0
ddr             	018C0000	00180000	0xff/0x1/0xff	0
apdp            	01A40000	00100000	0xff/0x1/0x0	0
xbl_config      	01B40000	00100000	0xff/0x1/0x0	0
multi_image     	01C40000	00100000	0xff/0x1/0x0	0
aop             	01D40000	00100000	0xff/0x1/0x0	0
qhee            	01E40000	00100000	0xff/0x1/0x0	0
abl             	01F40000	00100000	0xff/0x1/0x0	0
uefi            	02040000	00280000	0xff/0x1/0x0	0
toolsfv         	022C0000	00180000	0xff/0x1/0x0	0
loader_sti      	02440000	00180000	0xff/0x1/0x0	0
boot            	025C0000	00B40000	0xff/0x1/0x0	0
scrub           	03100000	00100000	0xff/0x1/0x0	0
modem           	03200000	04B40000	0xff/0x1/0x0	0
misc            	07D40000	001C0000	0xff/0x1/0x0	0
devinfo         	07F00000	00180000	0xff/0x1/0x0	0
recovery        	08080000	00B00000	0xff/0x1/0x0	0
fota            	08B80000	001C0000	0xff/0x1/0x0	0
recoveryfs      	08D40000	03000000	0xff/0x1/0x0	0
sec             	0BD40000	00100000	0xff/0x1/0x0	0
ztefile         	0BE40000	00A00000	0xff/0x1/0x0	0
zterw           	0C840000	09600000	0xff/0x1/0x0	0
system          	15E40000	0A1C0000	0xff/0x1/0x0	0
```

## Reading, erasing and writing partitions

Each time a partition is modified using EDL, re-writing the **SBL** *(secondary boot loader)* and partition layout (used re-calculate all CRCs) is necessary. To do this, this command can be used (use **SBL1+P-Layout** based on your QFIL package):

⚠️ **IF SBL1 AND PARTITONS LAYOUT ARE ERASED, YOUR UNIT WILL ALWAYS BOOT IN EDL MODE** ⚠️

Erase SBL1+Partition-Layout using this command:
```
edl es 0 639 --memory=NAND --sectorsize=4096 --loader=/path/to/prog_firehose.mbn
edl es 640 1279 --memory=NAND --sectorsize=4096 --loader=/path/to/prog_firehose.mbn
```

Write back SBL1+Partition-Layout using this command:
```
edl ws 640 partition_complete_p4K_b256K.mbn --memory=NAND --sectorsize=4096 --loader=/path/to/prog_firehose.mbn
edl ws 0 sbl1.mbn --memory=NAND --sectorsize=4096 --loader=/path/to/prog_firehose.mbn
```

Read a single partition using this command:
```
edl r system test_system.bin --memory=NAND --loader=/path/to/prog_firehose.mbn
```

Erase a single partition using this command:
```
edl e system --memory=NAND --loader=/path/to/prog_firehose.mbn
```

Write a single partition using this command:
```
edl w system system.bin --memory=NAND --loader=/path/to/prog_firehose.mbn
```

Make a backup of an entire partition using this command:
```
mkdir dump_dir
edl rl dump_dir --memory=NAND --loader=/path/to/prog_firehose.mbn
```
These files cannot be rewritten as is, they need to be refectored.

Reset the unit, making it boot back to normal mode, using this command:
```
edl reset --resetmode=reset --loader=/path/to/prog_firehose.mbn
```

In case the unit is stuck in DIAG mode (3 TTY), open an AT session to the relative port (usually `/dev/ttyUSB1` or `/dev/ttyUSB2`) and type:
```
AT+ZCDRUN=8
AT+ZCDRUN=F
AT+CFUN=1,1
```

# Force module to boot in FASTBOOT

Use these commands to erase `boot` partition and make module boots into ***fastboot*** mode

```
edl e boot --memory=NAND --loader=/path/to/prog_firehose.mbn
edl reset --resetmode=reset --loader=/path/to/prog_firehose.mbn
```

After you have erased ***boot*** partition, you can erase and write partitions with **fastboot** and avoid rewriting **SBL1** each time.
