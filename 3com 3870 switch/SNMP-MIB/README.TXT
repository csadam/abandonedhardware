
SuperStack(R) 3 Switch 38xx Family MIB Package 
for SW Agent Ver 2.0x Last updated 18th March 2005 


This document provides the following information:

1. 3Com Products and Software Agents compatible with this MIB Package
2. MIB files contained in this Package
3. Additional MIB files obtainable from 3Com Technical Support
4. Changes at this MIB Package
5. Recommendations when Loading MIB Files contained in this Package
6. 3Com's World Wide Web site
_____________________________________________________________________

1. 3Com Products and Software Agents compatible with this MIB package

This MIB package is compatible with the ver 2.0x agent feature
set for those products whose software agent filename is prefixed by
s3h02_0 

  
It provides support for the following SuperStack(R) 38xx family 
switches: 

Switch 3870-24             3CR17450-91
Switch 3870-48             3CR17451-91
Switch 3848                3CR17402-91

       3870  10 Gig Module 3C17706

_____________________________________________________________________


2. MIB Files contained in this package

Both IETF Standards based MIBs (RFCs) and 3Com proprietary MIBs are 
included in this package. MIB files marked with 

    * are not included in this package and you should contact 3Com  
      Technical Support for the latest versions. 
   ** are used to import definitions from, any operational mib items  
      defined within these files are not implemented.

MIB files marked as "Mandatory" contain definitions used by MIB files 
later in the loading sequence and as such should not be omitted. Other 
MIB files may be omitted but the functionality they control will then 
not be accessible via SNMP management.

IETF RFCs
                  RFC1213.mib      MIB II                     Mandatory
                **RFC2578.mib      SNMPv2-SMI                 Mandatory
                **RFC2579.mib      SNMPv2-TC                  Mandatory
                **ianaiftype.mib                              Mandatory
                **RFC1907.mib      SNMPv2-MIB                 Mandatory
                **RFC2580.mib      SNMPv2-CONF                Mandatory
                **RFC2571.mib      SNMP-Framework-MIB         Mandatory
                **RFC3291.mib      INET-Addresses             Mandatory
                  RFC2863.mib      If Table Extensions
		**RFC2213.mib      Integrated Services MIB    Mandatory
		**RFC3289.mib      DiffServ MIB               Mandatory
                  RFC1493.mib      Bridge MIB                 Mandatory
                  RFC2819.mib      RMON 
                **RFC1513.mib      RMON Token Ring            Mandatory
                  RFC2021.mib      RMON II Probe Config 
                  RFC2674.mib      Bridge Mib and Vlan Extensions 
                  RFC2668.mib      802.3 Mau 
                  RFC2665.mib      Etherlike MIB 
		  RFC2737.mib      Entity MIB 
IEEE MIBS
                 *IEEE802.3adLAG    Link Aggregation MIB
		 *IEEE802.1xPAE.mib Port Access Control MIB
                 

3Com Proprietary MIBs

                  3Com0045.mib     3Com Products MIB,       Mandatory
                  3Com0004.mib     3Com Generic Branches,   Mandatory
                  3Com0496.mib     3Com Switch 38xx MIB     
_____________________________________________________________________


3. Additional MIB Files obtainable from 3Com Technical Support

 
The definitions of the following 3Com proprietary MIBs are subject to 
change,for the latest version please contact 3Com Technical Support.
                  
 
No Mibs applicable to this package.

IEEE802.3adLAG  can be obtained from the following link
http://www.ieee802.org/3/publication/ad/IEEE8023-LAG-MIB.txt
_____________________________________________________________________

4. Changes at this MIB Package

This is the first release of the Mib package for the Switch 38xx 

Note:-

RFC2819 Supercedes RFC1757   "RMON"
RFC2863 Supercedes RFC2233   "IF-MIB"
RFC3291 Supercedes RFC2851   "INET_ADDRESS-MIB"

_____________________________________________________________________

5. Recommendations when loading MIB Files.

Depending on the MIB browser or Network Management Platform being
used, the MIB files may need to be loaded in the sequence 
listed in Section 2.

If you are using multiple types of 3Com products, make sure  that 

    . The most recent files (3Com004.mib & 3Com045.mib) are loaded 
      from one of the mib packages.

    . Where a mib file supercedes previous files, only use that file. 
      e.g. if 3Com0481 supercedes 3Com0049 only use 3Com0481.

HP Openview users are recommended to use the HP Openview Integration 
pack available from 3Com.   
_____________________________________________________________________

6. 3Com's World Wide Web site

Access the latest networking information on the 3Com Corporation World 
Wide Web site by entering our URL into your Internet browser:

http://www.3com.com/
   
_____________________________________________________________________

(R) means registered trademark.

3Com and SuperStack are registered trademarks of 3Com Corporation.

Other trademarks are the property of their respective owners.

Copyright (c) 2005 3Com Corporation. All Rights Reserved.


