# SW Revisions (Currently Known)

| SW Revision                                      | HW Revision | Description                                                                                                                              | Support VoLTE |
|--------------------------------------------------|-------------|------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| VDF_IT_MF289FMODV1.0.0B07 (Build Date: 2021-07-16) | A.T1        | The first hardware version sold in Italy, supporting both VoLTE/VoIP by changing parameters inside the module.                         | ✅            |
| VDF_IT_MF289F1MODV1.0.0B02 (Build Date: 2021-07-16) | A.T2        | The second hardware reversion sold in Italy, supporting only VoIP. It requires changing the `config` to enable the RJ-11 port when in `VOICE` mode. | ❌ (Not OOB) |
| VDF_DE_MF289FMODV1.0.0B07 (Build Date: 2021-04-28) | A.T1        | The first hardware version sold as "GigaCube" in Germany, supporting both VoLTE/VoIP by changing parameters inside the module. | ❌ (Not OOB) |
| VDF_DE_MF289F1MODV1.0.0B05 (Build Date: 2022-05-11) | A.T2        | The second hardware revision sold as "GigaCube" in Germany. It supports VoLTE/VoIP by changing parameters inside the modules and also supports B20 aggregation. | ✅  |
| TMO_PL_MF289F1MODV1.0.0B03 (Build Date: 2021-10-14) | A.T2        | The only known hardware revision sold in Poland, supporting both VoLTE/VoIP by changing parameters inside the module and into `EFS` partition. | ✅   |
| DNA_FI_MF289F1MODV1.0.0B11 (Build Date: 2022-05-25) | A.T2        | The only known hardware revision sold in Finland by DNA, voice seems disabled on EFS                                                  | ❌ (Not OOB)  |

Based on the router board (MF289F or MF289F1 - the main difference is the presence of a dedicated WiFi 5GHz for the first board), the module also has this nomenclature in the firmware name.

The Italian revision doesn't support B20 aggregation; you have to remove a prune file from the EFS. You can refer to this [link](https://forum.fibra.click/d/32421-zte-mf289f-vodafone-fwa-sblocco-aggregazione-b20-su-modello-vfit) for instructions (sorry, it's in Italian).

All other variants can be found on the [ZTE ECCN](https://www.zte.com.cn/global/about/eccn.html) site.
