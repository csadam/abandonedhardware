# 3Com 3870

This device is an OEM of the Accton ES-4625/4649/SMC8724ML3 series. There are 2 3com-specific changes:



- Serial port was changed from DB9 to RJ45
- Portnumbering was changing from vertical to horizontal. Take in account that the frontpanel numbering is no longer consistent when you flash an Edgecore Firmware in a 3com switch.
- Note that the pinout in the 3Com manual for the DB-9 to RJ45 cable is WRONG.  Working settings are 19200, 8N1, no flow control.  The cable only needs 3 wires:
  - DB-9 Pin 2 RX -- RJ-45 Pin 3 TX
  - DB-9 Pin 3 TX -- RJ-45 Pin SIX (YES, 6, not 2) RX
  - DB-9 Pin 5 GND - RJ-45 Pin 5 GND



```
---------    --------- 
|1|2|3|4|    |1|3|5|7|
--------- vs ---------
|5|6|7|8|    |2|4|6|8| 
---------    ---------
```



## Contents

## Backdoors

### Bootloader & Hidden menus

With CTRL-U, you can interrupt the bootloader. It'll ask for a password, which is 'sosupdate' for this device.

```
Loading Diagnostic Image File : Sw3870_diag_V3_1_0_1.bix
Diagnostics 3.1.0.1
User Mode

--- Performing Power-On Self Tests (POST) ---
UART Loopback Test ........... PASS
DRAM Test .................... PASS
Timer Test ................... PASS
PCI Device 1 Test ............ PASS
I2C Bus Initialization ....... PASS
Switch Int Loopback Test ..... PASS
Crossbar Int Loopback Test ... PASS
Fan Speed Test ............... PASS
Done All Pass.
------------------ DONE ---------------------

Password: sosupdate


File Name                         S/Up Type Size       Create Time
--------------------------------- ---- ---- ---------- -----------
$binary_cfg_file.bin                0   10     128000  24:00:41
$binary_cfg_file_internal.bin       0   10     128000  24:00:46
$logfile_1                          0    3         64  1193046:28:15
$logfile_2                          0    3         64  1193046:28:15
$watch_dog_log                      0    7         84  24:05:34
Factory_Default_Config.cfg          0    5        455  24:01:01
certificate                         0    8      32256  24:01:29
op1.bix                             0    2    4962016  24:24:43
op2.bix                             1    2    4542628  24:18:23
startup1.cfg                        1    5       5692  24:01:15
startup2.cfg                        0    5       8116  24:03:59
--------------------------------- ---- ---- ---------- ----------
Free Space : 22020096
[X]modem Download  [D]elete File  [S]et Startup File
[C]hange Baudrate  [Q]uit
Select>
Loading Runtime Image File : op1.bix
Runtime 3.0.10.0
```

It does not display the following debug messages during boot, but the functions are enabled:

```
Press Ctrl+] to override expected module version
Press Ctrl+[ to enable stkctrl debug message
Press Ctrl+P to do both
```

During the booting it asks:

```
Expected module version: 3.0.10.0
PCI unit 0: Dev 0x5690, Rev 0x03, Chip BCM5690_A2, Driver BCM5690_A0
PCI unit 1: Dev 0x5690, Rev 0x03, Chip BCM5690_A2, Driver BCM5690_A0
PCI unit 2: Dev 0x5690, Rev 0x03, Chip BCM5690_A2, Driver BCM5690_A0
PCI unit 3: Dev 0x5690, Rev 0x03, Chip BCM5690_A2, Driver BCM5690_A0
PCI unit 4: Dev 0x5670, Rev 0x02, Chip BCM5670_A1, Driver BCM5670_A0
PCI device BCM5690_A2 attached as unit 0.
PCI device BCM5690_A2 attached as unit 1.
PCI device BCM5690_A2 attached as unit 2.
PCI device BCM5690_A2 attached as unit 3.
PCI device BCM5670_A1 attached as unit 4.

1.Backdoor functions

Enter your choice:
```

If you press 1, you can enter the password 'acct0ncl1':

```
Please enter the password to enter backdoor function
password:
```

If you enter the password too early you get:

```
Only Master mode can enter Accton CLI backdoor
```

If you enter the password too late you get nothing, so I just paste the password many times during booting after pressing 1.

This enables a mostly intact and functional Accton CLI, reachable after booting from the 3Com menu with ctrl-g:

```
Select menu option: <ctrl-g>
Enter Accton CLI backdoor

Backdoor#?
Exec commands:
  calendar       Date and time information
  clear          Resets functions
  configure      Enters configuration mode
  copy           Copies from one file to another
  delete         Deletes a file
  dir            Lists files on the file system
  disable        Returns to normal mode from privileged mode
  disconnect     Terminates an SSH, Telnet, or console connection
  dot1x          Configures 802.1x port-based access control
  exit           Exits from privileged EXEC mode
  help           Description of the interactive help system
  ip             Internet protocol
  light          Lights LEDs to show unit information
  ping           Sends ICMP echo packets to other network nodes
  quit           Exits a CLI session
  reload         Halts and performs a warm restart
  show           Shows information
  spanning-tree  Specifies spanning tree configuration
  switch         Stacking commands for the switch in the stack
  whichboot      Shows which files booted on system power up

Backdoor#dir
          File name                        File type       Startup Size (byte)
 -------------------------------------     --------------  ------- -----------
 Unit1:
          Sw3870_diag_V3_1_0_1.bix         Boot-Rom Image  Y           830040
          op1.bix                          Operation Code  Y          4949836
          Factory_Default_Config.cfg       Config File     N               35
          startup1.cfg                     Config File     Y             8114
          startup2.cfg                     Config File     N             8149
 ---------------------------------------------------------------------------
                                                  Total free space:  25821184
Backdoor#show system
System Description: 3Com SuperStack 3 Switch 3870 48-port
System OID String: 1.3.6.1.4.1.43.1.8.44
System Information
 System Up Time:          0 days, 0 hours, 1 minutes, and 9.19 seconds
 System Name:             [NONE]
 System Location:         [NONE]
 System Contact:          [NONE]
 MAC Address (Unit1):     00-14-7C-B4-C4-4D
 Web Server:              Enabled
 Web Server Port:         80
 Web Secure Server:       Enabled
 Web Secure Server Port:  443
 Telnet Server:           Enable
 Telnet Server Port:      23
 Jumbo Frame:             Disabled

 POST Result:
UART Loopback Test ........... PASS
DRAM Test .................... PASS
Timer Test ................... PASS
PCI Device 1 Test ............ PASS
I2C Bus Initialization ....... PASS
Switch Int Loopback Test ..... PASS
Crossbar Int Loopback Test ... PASS
Fan Speed Test ............... PASS

Done All Pass.
Backdoor#show version
Unit 1
 Serial Number:           Y7EW6DEB4C44D
 Hardware Version:        R01
 EPLD Version:            1.01
 Number of Ports:         48
 Main Power Status:       Up
 Redundant Power Status:  Not present

Agent (Master)
 Unit ID:                 1
 Loader Version:          3.1.0.1
 Boot ROM Version:        3.1.0.1
 Operation Code Version:  3.0.10.0

Backdoor#conf
Backdoor(config)#interface VLAN 1
Backdoor(config-if)#IP address 192.0.1.0 255.255.255.0

 Accton CLI been disable. Please use 3COM CLI to set RIF.
Failed to set IP address on VLAN 1
Backdoor(config-if)#
```

There is also another backdoor. If you paste 'd3bug1191' a few times during startup, you get into:

```
----------------------------------------
Main menu of backdoor:

 * ipfilter
 * cos
 * acl
 * hrdrv
 * devhrdrv
 * TNPD
 * cli3com
 * HTTP
 * snmp
 * SSH
 * SNTP
 * TFTP
 * dns
 * smtp
 * sys_mgr
 * sysmgr
 * NETIF
 * NETCFG
 * IPCFG
 * ROUTE
 * ICMP
 * IP
 * P2MEM
 * IML
 * 802.1x
 * userauth
 * igmpsnp
 * GVRP
 * vlan
 * xstp
 * lacp
 * swctrl
 * cfgdb
 * leddrv
 * fs
 * lan
 * lhash
 * SYSFUN
 * MREF
 * MEM
 * nmtrdrv
 * AMTRDRV
 * devswdrv
 * swdrv
 * ISC
 * IUC
 * stkmgmt

 exit --- To exit from backdoor.

Key in the CSC name:
```

Which has some low-level things of its own:

```
Key in the CSC name: swdrv

==========SWDRV BackDoor Menu================

 0. Exit
 1. Port related
 2. Spawn Chip Task
 3. Enter Chip Backdoor
=================================================
     select =2
==========SWDRV BackDoor Menu================

 0. Exit
 1. Port related
 2. Spawn Chip Task
 3. Enter Chip Backdoor
=================================================
     select =3
Enter Broadcom backdoor
BCM.0> ?
help: "??" or "help" for summary
Commands common to all modes:
?              ??             BackGround     CASE           CD
COMBO          CONFig         CONSole        CoPy           DATE
DeBug          DIR            DmaRomTest     Echo           EDline
EXIT           EXPR           FLASHINIT      FOR            Help
HISTory        HOST           IF             JOBS           KILL
LOCal          LOG            LOOP           LS             MKDIR
MORe           MoVe           MTiMeout       NOEcho         Pause
PRINTENV       PWD            QUIT           RCCache        RCLoad
REBOOT         REName         RESET          RM             RMDIR
SAVE           SET            SETENV         SHell          SLeep
Version
Commands for current mode:
ADC            AGE            ARLmode        Attach         Auth
BaseBoard      BIST           BPDU           BTiMeout       CACHE
CellHDR        CHecK          CLEAR          CLOCKS         COS
CounTeR        DAC            DELete         DETach         DMux
DSCP           DTAG           Dump           EditReg        EGRess
Filter         Getreg         HASH           HeaderMode     I2C
IBDump         IFConfig       INIT           Insert         INTR
IPG            IPMC           L2             L2MODE         L3
LCDMSG         LED            LINKscan       LISTmem        Listreg
LOOKup         MCAST          MIRror         MmuConFiG      MODify
Modreg         MUXsel         NetStat        NVram          PacketWatcher
PBMP           PHY            PKTSpeed       POE            PORT
PortRate       PortStat       PROBE          PUTREG         PVlan
RATE           RegCMp         REMove         RXCfg          RXMon
SCHan          SEArch         Setreg         SFAPINIT       SHOW
SIZEGBP        SlotHDR        SOC            STG            STiMeout
SVL            SystemSnake    TEMPerature    TestClear      TestList
TestMode       TestParameters TestRun        TestSelect     TRUNK
TX             TXCount        TXSTArt        TXSTOp         VLAN
Write          XClocks        XModem         XQDump         XQErr
BCM.0>
```

### Password override

There's a master account whose password is based on a challenge on the switches MAC-address.



Tested on

- 3com 3812
- 3com 3870
- Edgecore ES4649

```
Example:
# arp -an | grep 10.0.1.2
? (10.0.1.2) at 00:0E:6A:CB:B4:41 [ether] on eth0
# perl accton.pl 000E6ACBB441
!!98DMlH
# telnet 10.0.1.2
Trying 10.0.1.2...
Connected to 10.0.1.2.
Escape character is '^]'.
Login: __super
Password: !!98DMlH

Menu options: -------3Com SuperStack 3 Switch 3824 24-port---------------------
 bridge              - Administer bridge-wide parameters
 feature             - Administer system features
 gettingStarted      - Basic device configuration
 logout              - Logout of the Command Line Interface
 physicalInterface   - Administer physical interfaces
 protocol            - Administer protocols
 security            - Administer security
 system              - Administer system-level functions
 trafficManagement   - Administer traffic management

Type ? for help.
--------------------------------testswitch (1)--------------------------------
Select menu option:
telnet> close
Connection closed.
```



## **Flashing Accton Firmware onto 3COM switches**

If you wish to flash an Edgecore firmware on to the switch, a firmware image (v3.1.1.88 dated 14-Oct-2008) is still available on the Accton web site (<http://beta.edge-core.com/DownDtl.asp?sno=FGAMIO&c=C>). This version is somewhat newer than the latest 3COM version available through the HP web site (v3.00s56p7 dated 20-Jun-2008 at <https://h10145.www1.hp.com/Downloads/SoftwareReleases.aspx?ProductNumber=JF061A&lang=en&cc=us&prodSeriesId=4177876>)

To load the firmware, follow these steps:

- use the CTRL-U backdoor listed above to enter the diagnostic command interface using Hyperterminal (or other terminal program) and a serial cable. After logging in with the 'sosupdate' password, you will receive a list of files stored on the flash filesystem.
- The runtime firmware has the suffix 'bix (in the example above, you see an op1.bix and op2.bix, with op2.bix marked as the startup firmware). If you have more than one BIX image, delete the bix image which is not marked as the startup image (this will usually be the smaller or older image file). You can only have 2 runtime images stored in flash, if you attempt to upload a 3rd the upload will fail, so it is necessary to delete one of the two, assuming you have two.
- Use XMODEM-1K to upload the Accton firmware. Once the upload completes, you will be prompted for a file name and a file type. The file type is Multiple. Name the file with the same name as what you deleted (e.g. if you deleted op1.bix, name the file you upload op1.bix).
- Mark the uploaded firmware as a startup image.
- Make note of which 'startup#.cfg' is the current startup image. Mark the 'Factory_Default_Configuration.cfg' as a startup image
- Power cycle (not just reboot).

The Accton firmware is command-line based through the terminal console, not menu based like the 3COM firmware, but the Accton firmware does offer a web interface for easy configuration.

You need to note the startup configuration file for the Accton firmware is not compatible with the 3COM startup configuration file. If you want to swap between running the 3com and Accton firmware, before you save your Accton configuration, take a 'dir' of the flash filesystem, and then 'copy' the startup#.cfg file marked as the startup image to the non-startup cfg file. In the example above, you would copy startup1.cfg to startup2.cfg so you have a backup of the 3COM startup configuration. This way, you can swap between the two firmwares and config files by booting into the Control-U backdoor and then simply mark the correct BIX and CFG files as 'startup'.



*<This article was downloaded from http://etherhack.wikia.com/wiki/3Com_3870>*