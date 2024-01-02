# SW revisions (currently known)

| SW Revision                                         | HW Revision | Description                                                                                                                                               | Support VoLTE |
|-----------------------------------------------------|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| VDF_IT_MF289FMODV1.0.0B07 (build date: 2021-07-16)  | A.T1        | First hardware version sold in Italy, it supports both VoLTE/VoIP changing parameters inside the module. Defualt mode is `VOIP`                                                    | ✅             |
| VDF_IT_MF289F1MODV1.0.0B02 (build date: 2021-07-16) | A.T2        | Second hardware version sold in Italy, it supports only VoIP, needs to change `config` to enable RJ-11 port when in `VOICE` mode                          | ❌ (Not OOB)   |
| VDF_DE_MF289F1MODV1.0.0B05 (build date: 2022-05-11) | A.T2        | Only known hardware revision sold as "GigaCube" in Germany, it supports VoLTE/VoIP changing parameters inside the modules, it also support B20 aggregation | ✅             |
| TMO_PL_MF289F1MODV1.0.0B03 (build date: 2021-10-14) | A.T2        | Only known hardware revision sold in Polan, it supports both VoLTE/VoIP changing parameters inside the module and into `EFS` partition                     | ✅             |

Italian revision doesn't support B20 aggregation, you have to remove a prune file from the EFS. You can refer to this [link](https://forum.fibra.click/d/32421-zte-mf289f-vodafone-fwa-sblocco-aggregazione-b20-su-modello-vfit) on how to do it (sorry, it's in Italian)

All other variants can be found on the [ZTE ECCN](https://www.zte.com.cn/global/about/eccn.html) site