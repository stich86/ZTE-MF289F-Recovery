# The specifications of the internal **MF289F/F1** module are as follows:

The [MF289F](https://ztedevices.com/en-gl/mf289f/) router is a 4G indoor unit produced by ZTE with that has an internal LTE modem with these specs:

- Network support: 4G LTE Networks TDD/FDD + WCDMA
- Chipset: Qualcomm SDX24 Platform
- CPU: 1x Cortex A7 up to 1.4GHz
- RAM: 256MB
- NAND: 512MB
- 4G LTE Cat: 20 downlink & 13 uplink
- 4G LTE Speed: 2Gbit downlink & 316Mbit uplink
- Connectivity:
    - USB over MiniPCIe Header, operates in two modes:
        - Normal mode with QMI+DIAG+ADB+NMEA
        - Mode with only DIAG+NMEA+AT
    - Flashing requires an adapter for your PC, such as [this one](https://www.amazon.it/wireless-scheda-adattatore-modulo-testing/dp/B00YAOL4NE/ref=sr_1_3?__mk_it_IT=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=JRM39EDJSU8Z&keywords=mini+pcie+to+usb+sim&qid=1704221380&sprefix=minipcie+to+usb+sim%2Caps%2C105&sr=8-3).
    - When the module is on its router board, the bus speed is 3.0, on the adapter, it operates at 2.0.


# Useful Stuff

- [Software Revision](swver.md)
- [Partition & Filesystem Info](fs.md)
- [LTE Combos](cacombo.md)
- [Play with EDL tools and partitions](edl.md)
- [Enter 'Emergency Download Mode' (EDL) if your module is bricked](enter_edl_brick.md)
- [Recovery module that is hard-bricked - WINDOWS ONLY](recovery_brick_windows.md)
- [Swap Firmware on the module](swap_firmware.md)
- [Enable VoLTE for a Provider that is not supported](enable_volte.md)

⚠️ Certain links in this repo will lead to other repositories which are not under my control.
You accept that I have no control over and accepts no liability in respect of materials, products or services available externally of this repo. ⚠️

Any help is really appreciated, feel free to open a PR to fix or add informations 😊
