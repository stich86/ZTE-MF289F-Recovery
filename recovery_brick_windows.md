# Recovery module from an hard brick (Windows only)

Before starting, be sure to have your module in ***EDL*** mode. If it cannot be enter it using `adb`, follow instruction to use the [short points](https://github.com/stich86/ZTE-MF289F-Recovery/blob/main/enter_edl_brick.md)
⚠️ Download and install [these](https://mega.nz/folder/C1w1WLTa#46TCvg4-rq123fTFxEEbdg) drivers, [QPST](https://qpsttool.com/qpst-tool-v2-7-496) and [TeraTerm](https://github.com/TeraTermProject/teraterm/releases/tag/v5.1) before connect the module to your pc ⚠️ 

You need to download `base QFIL package` from this [link](https://mega.nz/folder/q5xl0RCJ#DX-kzPZ3SzQBxm-Q5D1e9w), software version (with also dummy QCN file and `config` file) you want to run from[here](https://mega.nz/folder/KlhwlR5C#K0q2i7tdBYPFvdSESDUrPQ) 

After you have chosen which software version run, move the following files in the same folder of `base QFIL package`:

```
NON-HLOS.ubi
sdxpoorwills-boot.img  
sdxpoorwills-sysfs.ubi 
uefi.elf
```

Now click on `flash.cmd` file and enter the `9008` COM port (just the number). Let's wait until module is flashed, when complete the module will be rebooted.

If everything was fine, your module should appear in the **Device Manager** with `3 TTY MODE` (Modem Port, Diagnostic Port, NMEA Port) like this screen:

<img src="asset/modem_after_first_restore.png" alt="COM state after first restore" width="auto" height="auto">

Now it's time to restore EFS data using the `dummy_IMEI_vfde.qcn` file. This QCN contains dummy IMEI (all zeros), please refer to [EFS Professional](https://xdaforums.com/t/tool-updated-29-12-14-efs-professional-v2-1-80b-also-for-non-samsung-devices.1308546/) on how to load QCN and modify it, I will not give you instruction on how to do, sorry :-)

When your QCN is filled with your own IMEI, launch `Software Download` program, click on `Restore` tab, load your QCN (select QCN format and not XML one) and restore it. When process termiante, the module will be rebooted.

<img src="asset/restore_qcn_1.png" alt="Select Tab Restore and QCN" width="auto" height="auto">

<img src="asset/restore_qcn_2.png" alt="Restore it" width="auto" height="auto">

After module is back online, run `EFS Explorer` and copy `config` file into EFS root:

<img src="asset/efs_explorer_connect.png" alt="Back to 4.." width="auto" height="auto">

<img src="asset/efs_explorer_restore_config.png" alt="Back to 4.." width="auto" height="auto">

Open TeraTerm (or another terminal emulator) and connect to `NMEA` port, then run these commands to put modem back to `4 TTY + QMI` mode:

<img src="asset/teraterm_at_configuration.png" alt="Back to 4.." width="auto" height="auto">

```
AT+ZCDRUN=8
AT+ZCDRUN=F
AT+ZSNT=6,0,0
AT+CFUN=1,1
```

<img src="asset/teraterm_at_commands.png" alt="Back to 4.." width="auto" height="auto">

Last reboot and in less than two minutes module should be back in `4 TTY + QMI`. From now you can access it again with `adb`

Check if `config` and IMEI were written correctly launching again TeraTerm (or another terminal emulator), connect to `NMEA` port and issue `ATI` command:

<img src="asset/teraterm_ati.png" alt="Restored :-)" width="auto" height="auto">

That's it!
