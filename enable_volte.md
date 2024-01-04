# Enable VoLTE on not-supported Provider

You can enable VoLTE (Voice Over LTE) on this module for unsupported providers OOB by adding certain files to the EFS and ensuring the execution of specific AT commands

Prerequisites: This has been tested only with the `dummy_IMEI_vfde.qcn` QCN file and the **T-Mobile\Vodafone DE AT.2** `config` file, which enables the `RJ-11` port even when in `VOICE` mode. Therefore, before starting, you need to erase your EFS and follow all the necessary steps, as outlined in the [recovery guide](https://github.com/stich86/ZTE-MF289F-Recovery/blob/main/recovery_brick_windows.md#restore-module-configuration-efs-and-nv-items))


Once you have successfully uploaded the EFS configuration, attach the module to Windows and open `EFS Explorer`. Copy the contents of the [`data_efs_per_VoLTE` folder](https://github.com/stich86/ZTE-MF289F-Recovery/tree/main/data_efs_per_VoLTE) folder into the `/data` folder of EFS

--- PUT IMAGE ---

Open TeraTerm and connect to `NMEA` port, then run these commands:

```
AT+CGDCONT=2,"IPV4V6","ims" 
AT+CGDCONT=3,"IPV4V6","sos"
AT$QCPDPIMSCFGE=2,1
AT$QCPDPIMSCFGE=3,1
```

Verify that APNs and IMS configuration was really applied with these commands (and relative output):

**APN**
```
AT+CGDCONT?
+CGDCONT: 1,"IPV4V6","","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,0
+CGDCONT: 2,"IPV4V6","ims","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,0
+CGDCONT: 3,"IPV4V6","sos","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,0

OK
```

**IMS Configuration** (note the "1" after APN ID)
```
AT$QCPDPIMSCFGE?
$QCPDPIMSCFGE: 1 , 0 , 0 , 0
$QCPDPIMSCFGE: 2 , 1 , 0 , 0
$QCPDPIMSCFGE: 3 , 1 , 0 , 0

OK
```

Restart module with the usual AT command `AT+CFUN=1,1`

When module is back online, open again TeraTerm to `NMEA` port and check if `IMS APN` is connected and has an assigned IP with this command:

```
AT+CGCONTRDP
+CGCONTRDP: 2,5,ims,10.76.206.157,,,,10.178.76.2,10.178.77.194

OK
```

Now you can try make/receive call and check if the modem is still in 4G using usual OpenWRT tools (like amazing [3ginfo-lite](https://github.com/4IceG/luci-app-3ginfo-lite) from @4IceG)

Here is a recap table with all tests made by me and other guys using this mode. If you got success with other ISP, feel free to open an PR and add it:

| ISP                             | VoLTE Working                                                 | SW Version                                                                       |
|---------------------------------|---------------------------------------------------------------|----------------------------------------------------------------------------------|
| TIM (IT) and relative MVNO      | ✅ (OOB)                                                       | VDF_IT_MF289FMODV1.0.0B07  VDF_DE_MF289F1MODV1.0.0B05                            |
| Vodafone (IT) and relative MVNO | ✅ (needs this mod)                                            | VDF_IT_MF289FMODV1.0.0B07  VDF_DE_MF289F1MODV1.0.0B05 TMO_PL_MF289F1MODV1.0.0B03 |
| Wind (IT) and relative MVNO     | ✅ (needs this mod)                                            | VDF_IT_MF289FMODV1.0.0B07  VDF_DE_MF289F1MODV1.0.0B05 TMO_PL_MF289F1MODV1.0.0B03 |
| Iliad (IT)                      | ❌ (They don't support VoLTE, also 2G fall-back isn't working) | VDF_IT_MF289FMODV1.0.0B07  VDF_DE_MF289F1MODV1.0.0B05 TMO_PL_MF289F1MODV1.0.0B03 |
| Plus (PL)                       | ✅ (needs this mod)                                            | VDF_DE_MF289F1MODV1.0.0B05                                                       |
| Play (PL)                       | ✅ (needs this mod)                                            | VDF_DE_MF289F1MODV1.0.0B05                                                       |
| T-Mobile (PL)                   | ✅ (needs this mod)                                            | VDF_DE_MF289F1MODV1.0.0B05                                                       |