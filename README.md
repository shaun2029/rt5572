rt5572
======

Fixes for rt5572 tested with Linux 3.2 based on DPO_RT5572_LinuxSTA_2.6.1.3_20121022.tar.bz2

THe vendor driver for the rt5572 (rt5572sta) is unstable. I am uspporting a wireless adatper 
P-Link WDN3200 on Linux 3.2.

This is work related to linux support for the O2 Joggler.

3.2.58joggler1 #23 SMP Sun May 11 17:17:53 UTC 2014 i686 i686 i686 GNU/Linux

Using the TP-Link WDN3200 testing shows that there are frequent disconnects.

This is my attampt to solve these issues.

From the kernel log:


Sep 13 19:50:32 laptop1 kernel: ===>rt_ioctl_giwscan. 5(5) BSS returned, data->length = 1058
Sep 13 19:50:40 laptop1 kernel: ===>rt_ioctl_giwscan. 5(5) BSS returned, data->length = 1058
Sep 13 19:50:48 laptop1 kernel: ===>rt_ioctl_giwscan. 5(5) BSS returned, data->length = 1034
Sep 13 19:50:48 laptop1 kernel: ==>rt_ioctl_siwfreq::SIOCSIWFREQ(Channel=6)
Sep 13 19:51:00 laptop1 kernel: ===>rt_ioctl_giwscan. 5(5) BSS returned, data->length = 866
Sep 13 19:51:02 laptop1 kernel: ---> RTMPFreeTxRxRingMemory
Sep 13 19:51:02 laptop1 kernel: <--- RTMPFreeTxRxRingMemory
Sep 13 19:51:02 laptop1 kernel: RtmpAsicLoadFirmware: ver 21/21, sum cdf7/cdf7, mac cdf72100
Sep 13 19:51:02 laptop1 kernel: NICLoadFirmware: firmware loaded already
Sep 13 19:51:02 laptop1 kernel: <-- RTMPAllocTxRxRingMemory, Status=0
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60420!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60468!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b604b0!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b603d8!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60300!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60348!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2aad8!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b1a068!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b1a0b4!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2abc4!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2aa48!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2ab78!
Sep 13 19:51:02 laptop1 kernel: -->RTUSBVenderReset
Sep 13 19:51:02 laptop1 kernel: <--RTUSBVenderReset
Sep 13 19:51:02 laptop1 kernel: BBP_R254 = 80
Sep 13 19:51:02 laptop1 kernel: CfgSetCountryRegion():CountryRegion in eeprom was programmed
Sep 13 19:51:02 laptop1 kernel: CfgSetCountryRegion():CountryRegion in eeprom was programmed
Sep 13 19:51:02 laptop1 kernel: Key1Str is Invalid key length(0) or Type(0)
Sep 13 19:51:02 laptop1 kernel: Key2Str is Invalid key length(0) or Type(0)
Sep 13 19:51:02 laptop1 kernel: Key3Str is Invalid key length(0) or Type(0)
Sep 13 19:51:02 laptop1 kernel: Key4Str is Invalid key length(0) or Type(0)
Sep 13 19:51:02 laptop1 kernel: 1. Phy Mode = 0
Sep 13 19:51:02 laptop1 kernel: 2. Phy Mode = 0
Sep 13 19:51:02 laptop1 kernel: NVM is Efuse and its size =3c[3c0-3fb] 
Sep 13 19:51:02 laptop1 kernel: Power = a0a
Sep 13 19:51:02 laptop1 kernel: Power2 = e0e
Sep 13 19:51:02 laptop1 kernel: Power = a0a
Sep 13 19:51:02 laptop1 kernel: Power2 = e0e
Sep 13 19:51:02 laptop1 kernel: Power = a0a
Sep 13 19:51:02 laptop1 kernel: Power2 = e0e
Sep 13 19:51:02 laptop1 kernel: Power = b0b
Sep 13 19:51:02 laptop1 kernel: Power2 = e0e
Sep 13 19:51:02 laptop1 kernel: Power = b0b
Sep 13 19:51:02 laptop1 kernel: Power2 = e0e
Sep 13 19:51:02 laptop1 kernel: Power = b0b
Sep 13 19:51:02 laptop1 kernel: Power2 = e0e
Sep 13 19:51:02 laptop1 kernel: 3. Phy Mode = 0
Sep 13 19:51:02 laptop1 kernel: [mAntCfgInit: primary/secondary ant 0/1
Sep 13 19:51:02 laptop1 kernel: [mbAutoTxAgcG = 0
Sep 13 19:51:02 laptop1 kernel: ---> InitFrequencyCalibration
Sep 13 19:51:02 laptop1 kernel: InitFrequencyCalibration: frequency offset in the EEPROM = 44
Sep 13 19:51:02 laptop1 kernel: <--- InitFrequencyCalibration
Sep 13 19:51:02 laptop1 kernel: RTMPSetPhyMode: channel is out of range, use first channel=1 
Sep 13 19:51:02 laptop1 kernel: MCS Set = 00 00 00 00 00
Sep 13 19:51:02 laptop1 kernel: <==== rt28xx_init, Status=0
Sep 13 19:51:02 laptop1 kernel: 0x1300 = 000a4200
Sep 13 19:51:02 laptop1 kernel: BIRIdx(0): RXDMALen not multiple of 4.[12387], BulkInBufLen = 260)
Sep 13 19:51:02 laptop1 kernel: ---> RTMPFreeTxRxRingMemory
Sep 13 19:51:02 laptop1 kernel: <--- RTMPFreeTxRxRingMemory
Sep 13 19:51:02 laptop1 kernel: RtmpAsicLoadFirmware: ver 21/21, sum cdf7/cdf7, mac cdf72100
Sep 13 19:51:02 laptop1 kernel: NICLoadFirmware: firmware loaded already
Sep 13 19:51:02 laptop1 kernel: <-- RTMPAllocTxRxRingMemory, Status=0
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60420!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60468!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b604b0!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b603d8!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60300!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60348!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2aad8!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b1a068!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b1a0b4!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2abc4!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2aa48!
Sep 13 19:51:02 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2ab78!
Sep 13 19:51:02 laptop1 kernel: -->RTUSBVenderReset
Sep 13 19:51:02 laptop1 kernel: <--RTUSBVenderReset
Sep 13 19:51:03 laptop1 kernel: BBP_R254 = 80
Sep 13 19:51:03 laptop1 kernel: CfgSetCountryRegion():CountryRegion in eeprom was programmed
Sep 13 19:51:03 laptop1 kernel: CfgSetCountryRegion():CountryRegion in eeprom was programmed
Sep 13 19:51:03 laptop1 kernel: Key1Str is Invalid key length(0) or Type(0)
Sep 13 19:51:03 laptop1 kernel: Key2Str is Invalid key length(0) or Type(0)
Sep 13 19:51:03 laptop1 kernel: Key3Str is Invalid key length(0) or Type(0)
Sep 13 19:51:03 laptop1 kernel: Key4Str is Invalid key length(0) or Type(0)
Sep 13 19:51:03 laptop1 kernel: 1. Phy Mode = 0
Sep 13 19:51:03 laptop1 kernel: 2. Phy Mode = 0
Sep 13 19:51:03 laptop1 kernel: NVM is Efuse and its size =3c[3c0-3fb] 
Sep 13 19:51:03 laptop1 kernel: Power = a0a
Sep 13 19:51:03 laptop1 kernel: Power2 = e0e
Sep 13 19:51:03 laptop1 kernel: Power = a0a
Sep 13 19:51:03 laptop1 kernel: Power2 = e0e
Sep 13 19:51:03 laptop1 kernel: Power = a0a
Sep 13 19:51:03 laptop1 kernel: Power2 = e0e
Sep 13 19:51:03 laptop1 kernel: Power = b0b
Sep 13 19:51:03 laptop1 kernel: Power2 = e0e
Sep 13 19:51:03 laptop1 kernel: Power = b0b
Sep 13 19:51:03 laptop1 kernel: Power2 = e0e
Sep 13 19:51:03 laptop1 kernel: Power = b0b
Sep 13 19:51:03 laptop1 kernel: Power2 = e0e
Sep 13 19:51:03 laptop1 kernel: 3. Phy Mode = 0
Sep 13 19:51:03 laptop1 kernel: [mAntCfgInit: primary/secondary ant 0/1
Sep 13 19:51:03 laptop1 kernel: [mbAutoTxAgcG = 0
Sep 13 19:51:03 laptop1 kernel: ---> InitFrequencyCalibration
Sep 13 19:51:03 laptop1 kernel: InitFrequencyCalibration: frequency offset in the EEPROM = 44
Sep 13 19:51:03 laptop1 kernel: <--- InitFrequencyCalibration
Sep 13 19:51:03 laptop1 kernel: RTMPSetPhyMode: channel is out of range, use first channel=1 
Sep 13 19:51:03 laptop1 kernel: MCS Set = 00 00 00 00 00
Sep 13 19:51:03 laptop1 kernel: <==== rt28xx_init, Status=0
Sep 13 19:51:03 laptop1 kernel: 0x1300 = 000a4200
Sep 13 19:51:03 laptop1 kernel: ---> RTMPFreeTxRxRingMemory
Sep 13 19:51:03 laptop1 kernel: <--- RTMPFreeTxRxRingMemory
Sep 13 19:51:03 laptop1 kernel: r8168: eth0: link down
Sep 13 19:51:06 laptop1 kernel: RtmpAsicLoadFirmware: ver 21/21, sum cdf7/cdf7, mac cdf72100
Sep 13 19:51:06 laptop1 kernel: NICLoadFirmware: firmware loaded already
Sep 13 19:51:06 laptop1 kernel: <-- RTMPAllocTxRxRingMemory, Status=0
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60420!
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60468!
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b604b0!
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b603d8!
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60300!
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b60348!
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2aad8!
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b1a068!
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b1a0b4!
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2abc4!
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2aa48!
Sep 13 19:51:06 laptop1 kernel: RTMP_TimerListAdd: add timer obj f1b2ab78!
Sep 13 19:51:06 laptop1 kernel: -->RTUSBVenderReset
Sep 13 19:51:06 laptop1 kernel: <--RTUSBVenderReset
Sep 13 19:51:07 laptop1 kernel: BBP_R254 = 80
Sep 13 19:51:07 laptop1 kernel: CfgSetCountryRegion():CountryRegion in eeprom was programmed
Sep 13 19:51:07 laptop1 kernel: CfgSetCountryRegion():CountryRegion in eeprom was programmed
Sep 13 19:51:07 laptop1 kernel: Key1Str is Invalid key length(0) or Type(0)
Sep 13 19:51:07 laptop1 kernel: Key2Str is Invalid key length(0) or Type(0)
Sep 13 19:51:07 laptop1 kernel: Key3Str is Invalid key length(0) or Type(0)
Sep 13 19:51:07 laptop1 kernel: Key4Str is Invalid key length(0) or Type(0)
Sep 13 19:51:07 laptop1 kernel: 1. Phy Mode = 0
Sep 13 19:51:07 laptop1 kernel: 2. Phy Mode = 0

