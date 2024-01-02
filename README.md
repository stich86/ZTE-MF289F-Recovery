# This is a repository with all informations about ZTE MF289/MF289F1 internal LTE module

The [MF289F](https://ztedevices.com/en-gl/mf289f/) router is a 4G indor unit produced by ZTE with that has an internal LTE modem with these specs:

- Network support: 4G LTE Networks TDD/FDD + WCDMA
- Chipset: Qualcomm SDX24 Platform
- CPU: 1x Cortex A7 up to 1.4GHz
- RAM: 256MB
- NAND: 512MB
- 4G LTE Cat: 20
- Network connectivity: 2.5GbE interface with PoE 802.3af/at (bundled injector)
- Connectivity:
    - USB over MiniPCIe Header, runs two modes, one normal with QMI+DIAG+ADB+NMEA and one with just DIAG+NMEA+AT. You need an adapter to flash it on your PC like [this](https://www.amazon.it/wireless-scheda-adattatore-modulo-testing/dp/B00YAOL4NE/ref=sr_1_3?__mk_it_IT=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=JRM39EDJSU8Z&keywords=mini+pcie+to+usb+sim&qid=1704221380&sprefix=minipcie+to+usb+sim%2Caps%2C105&sr=8-3)

# Useful Stuff

- [Software Revision](swver.md)
- [Partition & Filesystem Info](fs.md)
- [LTE Combos](cacombo.md)
- [Play with EDL tools and partitions](edl.md)
- [Enter 'Emergency Download Mode' (EDL) if your module is bricked](enter_edl_brick.md)
- [Recovery module that is hard-bricked - WINDOWS ONLY](recovery_brick_windows.md)

⚠️ Certain links in this repo will lead to other repositories which are not under my control.
You accept that I have no control over and accepts no liability in respect of materials, products or services available externally of this repo. ⚠️

Any help is really appreciated, feel free to open a PR to fix or add informations 😊
