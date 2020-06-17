
# Maîtrise de poste - Day 1

## Self-footprinting

### Host OS

Déterminer les principales informations de votre machine:

nom de la machine :
```
PS C:\Users\sacha> [system.environment]::MachineName
LAPTOP-DPNRPKUF
```
OS et version :
```
PS C:\Users\sacha> wmic OS get Name
Name
Microsoft Windows 10 Famille|C:\WINDOWS|\Device\Harddisk1\Partition3

PS C:\Users\sacha> wmic OS get Version
Version
10.0.18363
```
architecture processeur (32-bit, 64-bit, ARM, etc) :
```
PS C:\Users\sacha> Get-WmiObject Win32_OperatingSystem | Select-Object OSArchitecture

OSArchitecture
--------------
64 bits

```
modèle du processeur :
```
PS C:\Users\sacha> wmic CPU get DataWidth
DataWidth
64
```
quantité RAM et modèle de la RAM :
```
PS C:\Users\sacha> wmic MEMORYCHIP get Manufacturer
Manufacturer
SK Hynix
SK Hynix

PS C:\Users\sacha> wmic MEMORYCHIP get Capacity
Capacity
8589934592
8589934592
```

### Devices

Trouver:

la marque et le modèle de votre processeur:

```
PS C:\Users\sacha> wmic CPU get Name
Name
Intel(R) Core(TM) i7-9750H CPU @ 2.60GHz
```



Disque dur principal

```
PS C:\Users\sacha> wmic DISKDRIVE get MODEL
Model
WDC PC SN520 SDAPNUW-512G-1014
WDC WD10SPZX-21Z10T0
```

Disque dur:

Partition:

```
PS C:\Users\sacha> Get-Partition


   DiskPath : \\?\scsi#disk&ven_nvme&prod_wdc_pc_sn520_sda#4&200c0aff&0&010000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}

PartitionNumber  DriveLetter Offset                                        Size Type
---------------  ----------- ------                                        ---- ----
1                            1048576                                     100 MB System
2                            105906176                                    16 MB Reserved
3                C           122683392                                475.82 GB Basic
4                            511027707904                                  1 GB Recovery


   DiskPath : \\?\scsi#disk&ven_wdc&prod_wd10spzx-21z10t0#4&200c0aff&0&000400#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}

PartitionNumber  DriveLetter Offset                                        Size Type
---------------  ----------- ------                                        ---- ----
1                D           1048576                                  931.51 GB Basic


PS C:\Users\sacha>
```

Le premier sert à héberger le système d'exploitation.
Le deuxieme est un reserved.
Le troisième permet de stock des install sur le pc (basic)
Le 4ème permet de faire des sauvegardes de la machine.

### Network

Liste des cartes réseau:
```
PS C:\Users\sacha> Get-NetAdapter | fl Name, InterfaceIndex


Name           : VirtualBox Host-Only Network #8
InterfaceIndex : 89

Name           : Ethernet 2
InterfaceIndex : 26

Name           : VirtualBox Host-Only Network #4
InterfaceIndex : 24

Name           : VirtualBox Host-Only Network #6
InterfaceIndex : 79

Name           : Connexion réseau Bluetooth
InterfaceIndex : 23

Name           : Ethernet 3
InterfaceIndex : 17

Name           : VirtualBox Host-Only Network #5
InterfaceIndex : 74

Name           : Ethernet 4
InterfaceIndex : 15

Name           : Ethernet
InterfaceIndex : 14

Name           : VMware Network Adapter VMnet8
InterfaceIndex : 7

Name           : Wi-Fi
InterfaceIndex : 4

Name           : VMware Network Adapter VMnet1
InterfaceIndex : 2

Name           : VirtualBox Host-Only Network #7
InterfaceIndex : 84

```
Il y a les  4 ETHERNET, la carte WIFI, les vm de virtualbox, les vm de VMware et la connexion bluethooth.

```
PS C:\WINDOWS\system32> netstat -abo

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    0.0.0.0:80             LAPTOP-DPNRPKUF:0      LISTENING       4
 Impossible d’obtenir les informations de propriétaire
  TCP    0.0.0.0:135            LAPTOP-DPNRPKUF:0      LISTENING       104
  RpcSs
 [svchost.exe]
  TCP    0.0.0.0:443            LAPTOP-DPNRPKUF:0      LISTENING       20916
 [httpd.exe]
  TCP    0.0.0.0:445            LAPTOP-DPNRPKUF:0      LISTENING       4
 Impossible d’obtenir les informations de propriétaire
  TCP    0.0.0.0:902            LAPTOP-DPNRPKUF:0      LISTENING       4840
 [vmware-authd.exe]
  TCP    0.0.0.0:912            LAPTOP-DPNRPKUF:0      LISTENING       4840
 [vmware-authd.exe]
  TCP    0.0.0.0:3306           LAPTOP-DPNRPKUF:0      LISTENING       11956
 [mysqld.exe]
  TCP    0.0.0.0:5040           LAPTOP-DPNRPKUF:0      LISTENING       644
  CDPSvc
 [svchost.exe]
  TCP    0.0.0.0:5357           LAPTOP-DPNRPKUF:0      LISTENING       4
 Impossible d’obtenir les informations de propriétaire
  TCP    0.0.0.0:7680           LAPTOP-DPNRPKUF:0      LISTENING       848
 Impossible d’obtenir les informations de propriétaire
  TCP    0.0.0.0:8080           LAPTOP-DPNRPKUF:0      LISTENING       20916
 [httpd.exe]
  TCP    0.0.0.0:29320          LAPTOP-DPNRPKUF:0      LISTENING       20048
 [Spotify.exe]
  TCP    0.0.0.0:49664          LAPTOP-DPNRPKUF:0      LISTENING       900
 [lsass.exe]
  TCP    0.0.0.0:49665          LAPTOP-DPNRPKUF:0      LISTENING       808
 Impossible d’obtenir les informations de propriétaire
  TCP    0.0.0.0:49666          LAPTOP-DPNRPKUF:0      LISTENING       1832
  EventLog
 [svchost.exe]
  TCP    0.0.0.0:49667          LAPTOP-DPNRPKUF:0      LISTENING       2708
  SessionEnv
 [svchost.exe]
  TCP    0.0.0.0:49668          LAPTOP-DPNRPKUF:0      LISTENING       2564
  Schedule
 [svchost.exe]
  TCP    0.0.0.0:49669          LAPTOP-DPNRPKUF:0      LISTENING       3644
 [spoolsv.exe]
  TCP    0.0.0.0:49673          LAPTOP-DPNRPKUF:0      LISTENING       4336
  PolicyAgent
 [svchost.exe]
  TCP    0.0.0.0:49676          LAPTOP-DPNRPKUF:0      LISTENING       880
 Impossible d’obtenir les informations de propriétaire
  TCP    0.0.0.0:57621          LAPTOP-DPNRPKUF:0      LISTENING       20048
 [Spotify.exe]
  TCP    10.2.1.1:139           LAPTOP-DPNRPKUF:0      LISTENING       4
 Impossible d’obtenir les informations de propriétaire
  TCP    11.11.11.1:139         LAPTOP-DPNRPKUF:0      LISTENING       4
 Impossible d’obtenir les informations de propriétaire
  TCP    12.12.12.1:139         LAPTOP-DPNRPKUF:0      LISTENING       4
 Impossible d’obtenir les informations de propriétaire
  TCP    13.13.13.1:139         LAPTOP-DPNRPKUF:0      LISTENING       4
 Impossible d’obtenir les informations de propriétaire
  TCP    127.0.0.1:6463         LAPTOP-DPNRPKUF:0      LISTENING       20436
 [Discord.exe]
  TCP    127.0.0.1:15292        LAPTOP-DPNRPKUF:0      LISTENING       20180
 [Adobe Desktop Service.exe]
  TCP    127.0.0.1:15393        LAPTOP-DPNRPKUF:0      LISTENING       20180
 [Adobe Desktop Service.exe]
  TCP    127.0.0.1:16494        LAPTOP-DPNRPKUF:0      LISTENING       20180
 [Adobe Desktop Service.exe]
  TCP    127.0.0.1:18301        LAPTOP-DPNRPKUF:0      LISTENING       1804
 [node.exe]
  TCP    127.0.0.1:18301        LAPTOP-DPNRPKUF:27313  ESTABLISHED     1804
 [node.exe]
  TCP    127.0.0.1:18304        LAPTOP-DPNRPKUF:0      LISTENING       1804
 [node.exe]
  TCP    127.0.0.1:18307        LAPTOP-DPNRPKUF:0      LISTENING       1804
 [node.exe]
  TCP    127.0.0.1:27313        LAPTOP-DPNRPKUF:18301  ESTABLISHED     10764
 [Adobe CEF Helper.exe]
  TCP    127.0.0.1:45623        LAPTOP-DPNRPKUF:0      LISTENING       1804
 [node.exe]
  TCP    127.0.0.1:49894        LAPTOP-DPNRPKUF:0      LISTENING       10136
 [NVIDIA Web Helper.exe]
  TCP    127.0.0.1:65001        LAPTOP-DPNRPKUF:0      LISTENING       3448
 [nvcontainer.exe]
  TCP    169.254.159.28:139     LAPTOP-DPNRPKUF:0      LISTENING       4
 Impossible d’obtenir les informations de propriétaire
  TCP    192.168.1.41:139       LAPTOP-DPNRPKUF:0      LISTENING       4
 Impossible d’obtenir les informations de propriétaire
  TCP    192.168.1.41:25523     a23-54-61-109:https    CLOSE_WAIT      16948
 [Microsoft.Msn.News.exe]
  TCP    192.168.1.41:27334     162.159.133.234:https  ESTABLISHED     11660
 [Discord.exe]
  TCP    192.168.1.41:27381     wo-in-f188:https       ESTABLISHED     24620
 [chrome.exe]
  TCP    192.168.1.41:27514     52.114.77.96:https     ESTABLISHED     16896
 [Teams.exe]
  TCP    192.168.1.41:27523     47:https               ESTABLISHED     11660
 [Discord.exe]
  TCP    192.168.1.41:27552     ec2-63-32-157-172:https  ESTABLISHED     17764
 [CoreSync.exe]
  TCP    192.168.1.41:27566     40.67.254.36:https     ESTABLISHED     3804
  WpnService
 [svchost.exe]
  TCP    192.168.1.41:27709     52.109.88.8:https      ESTABLISHED     24916
 [HxOutlook.exe]
  TCP    192.168.1.41:29088     ec2-54-64-181-150:https  ESTABLISHED     24620
 [chrome.exe]
  TCP    192.168.1.41:29114     52.97.233.34:imaps     ESTABLISHED     10172
  OneSyncSvc_9ab5ed
 [svchost.exe]
  TCP    192.168.1.41:29195     162.159.130.235:https  ESTABLISHED     11660
 [Discord.exe]
  TCP    192.168.1.41:29237     162.159.135.233:https  ESTABLISHED     11660
 [Discord.exe]
  TCP    192.168.1.41:29336     58:4070                ESTABLISHED     20048
 [Spotify.exe]
  TCP    192.168.1.41:29337     53:https               ESTABLISHED     9832
 [Spotify.exe]
  TCP    192.168.1.41:29347     47:https               ESTABLISHED     20048
 [Spotify.exe]
  TCP    192.168.1.41:29355     151.101.122.248:https  ESTABLISHED     9832
 [Spotify.exe]
  TCP    192.168.1.41:29356     151.101.122.248:https  ESTABLISHED     9832
 [Spotify.exe]
  TCP    192.168.1.41:29357     151.101.122.248:https  ESTABLISHED     9832
 [Spotify.exe]
  TCP    192.168.1.41:29358     151.101.122.248:https  ESTABLISHED     9832
 [Spotify.exe]
  TCP    192.168.1.41:29359     151.101.122.248:https  ESTABLISHED     9832
 [Spotify.exe]
  TCP    192.168.1.41:29366     151.101.122.248:https  ESTABLISHED     9832
 [Spotify.exe]
  TCP    192.168.1.41:29367     151.101.122.248:https  ESTABLISHED     9832
 [Spotify.exe]
  TCP    192.168.1.41:29368     151.101.122.248:https  ESTABLISHED     9832
 [Spotify.exe]
  TCP    192.168.1.41:29369     151.101.122.248:https  ESTABLISHED     9832
 [Spotify.exe]
  TCP    192.168.1.41:29370     151.101.122.248:https  ESTABLISHED     9832
 [Spotify.exe]
  TCP    192.168.1.41:29371     151.101.122.248:https  ESTABLISHED     9832
 Impossible d’obtenir les informations de propriétaire
  TCP    192.168.1.41:29372     151.101.122.248:https  ESTABLISHED     9832
 Impossible d’obtenir les informations de propriétaire
  TCP    192.168.1.41:29374     151.101.122.248:https  ESTABLISHED     9832
 Impossible d’obtenir les informations de propriétaire
  TCP    192.168.1.41:29376     151.101.122.248:https  ESTABLISHED     9832
 Impossible d’obtenir les informations de propriétaire
  TCP    192.168.1.41:29425     25:https               ESTABLISHED     11660
 [Discord.exe]
  TCP    192.168.1.41:29452     151.101.122.248:https  ESTABLISHED     9832
 Impossible d’obtenir les informations de propriétaire

```

Les ports TCP qui sont ESTABLISHED sont soit pour des programmes, des processus de Windows et les UDP sont pour certains processus windows.

### Users

Déterminer la liste des utilisateurs de la machine:

```
PS C:\WINDOWS\system32> net user

comptes d’utilisateurs de \\LAPTOP-DPNRPKUF

-------------------------------------------------------------------------------
Administrateur           DefaultAccount           Invité
sacha                    WDAGUtilityAccount       YNOV01
YNOV02                   YNOV03                   YNOV04
YNOV05                   YNOV06                   YNOV07
YNOV08                   YNOV09                   YNOV10
YNOV11                   YNOV12                   YNOV13
YNOV14                   YNOV15                   YNOV16
YNOV17                   YNOV18                   YNOV19
YNOV20
La commande s’est terminée correctement.
```
```

PS C:\WINDOWS\system32> net user sacha
Nom d’utilisateur                              sacha
Nom complet
Commentaire
Commentaires utilisateur
Code du pays ou de la région                   000 (Valeur par défaut du système)
Compte : actif                                 Oui
Le compte expire                               Jamais

Mot de passe : dernier changmt.                ‎17/‎09/‎2019 20:17:21
Le mot de passe expire                         Jamais
Le mot de passe modifiable                     ‎17/‎09/‎2019 20:17:21
Mot de passe exigé                             Oui
L’utilisateur peut changer de mot de passe     Oui

Stations autorisées                            Tout
Script d’ouverture de session
Profil d’utilisateur
Répertoire de base
Dernier accès                                  Jamais

Heures d’accès autorisé                        Tout

Appartient aux groupes locaux                  *Administrateurs
                                               *HelpLibraryUpdaters
                                               *Utilisateurs
                                               *Utilisateurs du journ
Appartient aux groupes globaux                 *Aucun
La commande s’est terminée correctement.

PS C:\WINDOWS\system32>
```

### Processus

Déterminer la liste des processus de la machine :

```
PS C:\WINDOWS\system32> tasklist

Nom de l’image                 PID Nom de la sessio Numéro de s Utilisation
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0         8 Ko
System                           4 Services                   0     2 316 Ko
Registry                       144 Services                   0    62 080 Ko
smss.exe                       544 Services                   0       396 Ko
csrss.exe                      632 Services                   0     2 140 Ko
wininit.exe                    808 Services                   0     1 036 Ko
csrss.exe                      816 Console                    1     3 160 Ko
services.exe                   880 Services                   0     6 948 Ko
lsass.exe                      900 Services                   0    16 884 Ko
svchost.exe                   1020 Services                   0     1 276 Ko
svchost.exe                    108 Services                   0    32 196 Ko
fontdrvhost.exe                572 Services                   0       736 Ko
WUDFHost.exe                   600 Services                   0     1 504 Ko
svchost.exe                    104 Services                   0    29 548 Ko
svchost.exe                   1068 Services                   0     4 744 Ko
winlogon.exe                  1188 Console                    1     4 556 Ko
fontdrvhost.exe               1240 Console                    1     4 300 Ko
svchost.exe                   1360 Services                   0     4 568 Ko
svchost.exe                   1400 Services                   0     2 828 Ko
svchost.exe                   1408 Services                   0     4 812 Ko
svchost.exe                   1420 Services                   0     6 268 Ko
svchost.exe                   1584 Services                   0     5 648 Ko
svchost.exe                   1592 Services                   0     5 224 Ko
svchost.exe                   1692 Services                   0     4 424 Ko
svchost.exe                   1740 Services                   0     3 764 Ko
svchost.exe                   1784 Services                   0     2 112 Ko
svchost.exe                   1832 Services                   0    11 388 Ko
svchost.exe                   2016 Services                   0     5 220 Ko
svchost.exe                   2024 Services                   0     9 992 Ko
svchost.exe                   2032 Services                   0     4 172 Ko
NVDisplay.Container.exe       1932 Services                   0     5 696 Ko
svchost.exe                   2056 Services                   0     4 736 Ko
svchost.exe                   2064 Services                   0     4 424 Ko
dasHost.exe                   2120 Services                   0     7 140 Ko
svchost.exe                   2160 Services                   0     5 640 Ko
svchost.exe                   2244 Services                   0     6 328 Ko
svchost.exe                   2252 Services                   0     1 692 Ko
svchost.exe                   2272 Services                   0     3 528 Ko
svchost.exe                   2384 Services                   0    10 188 Ko
svchost.exe                   2432 Services                   0     3 176 Ko
Memory Compression            2480 Services                   0   894 476 Ko
svchost.exe                   2548 Services                   0     4 964 Ko
svchost.exe                   2556 Services                   0    16 012 Ko
svchost.exe                   2564 Services                   0    10 788 Ko
svchost.exe                   2708 Services                   0     3 428 Ko
igfxCUIService.exe            2720 Services                   0     1 764 Ko
svchost.exe                   2796 Services                   0     6 836 Ko
svchost.exe                   2860 Services                   0     5 972 Ko
svchost.exe                   2872 Services                   0     4 296 Ko
svchost.exe                   3004 Services                   0     6 660 Ko
svchost.exe                   3104 Services                   0    10 580 Ko
svchost.exe                   3224 Services                   0     3 016 Ko
svchost.exe                   3232 Services                   0     5 652 Ko
svchost.exe                   3424 Services                   0    11 552 Ko
svchost.exe                   3508 Services                   0     6 556 Ko
spoolsv.exe                   3644 Services                   0    13 196 Ko
svchost.exe                   3700 Services                   0     7 136 Ko
svchost.exe                   3728 Services                   0     9 668 Ko
svchost.exe                   3820 Services                   0     2 504 Ko
svchost.exe                   4056 Services                   0    42 592 Ko
svchost.exe                   4064 Services                   0    25 388 Ko
IntelCpHDCPSvc.exe            4072 Services                   0     1 588 Ko
ACCSvc.exe                    4084 Services                   0     1 456 Ko
svchost.exe                   4092 Services                   0    51 544 Ko
svchost.exe                   2980 Services                   0     4 048 Ko
IntelAudioService.exe         3360 Services                   0     9 276 Ko
svchost.exe                   3396 Services                   0     1 628 Ko
nvcontainer.exe               3448 Services                   0    18 248 Ko
svchost.exe                   3804 Services                   0    13 884 Ko
RstMwService.exe              3760 Services                   0       932 Ko
RtkAudUService64.exe          4108 Services                   0     3 776 Ko
vmnetdhcp.exe                 4120 Services                   0     1 052 Ko
svchost.exe                   4128 Services                   0    39 216 Ko
svchost.exe                   4136 Services                   0     2 108 Ko
vmnat.exe                     4144 Services                   0     2 128 Ko
LMS.exe                       4152 Services                   0     2 668 Ko
svchost.exe                   4168 Services                   0     9 096 Ko
sqlwriter.exe                 4176 Services                   0     1 700 Ko
svchost.exe                   4336 Services                   0     4 192 Ko
svchost.exe                   4372 Services                   0     4 720 Ko
svchost.exe                   4540 Services                   0     3 532 Ko
IntelCpHeciSvc.exe            4676 Services                   0     1 612 Ko
svchost.exe                   4832 Services                   0    43 596 Ko
vmware-authd.exe              4840 Services                   0     4 744 Ko
vmware-usbarbitrator64.ex     4884 Services                   0     3 332 Ko
svchost.exe                   4892 Services                   0     1 512 Ko
sqlservr.exe                  5048 Services                   0    90 152 Ko
sqlceip.exe                   5056 Services                   0    24 512 Ko
ReportingServicesService.     5064 Services                   0    54 796 Ko
jhi_service.exe               4284 Services                   0       996 Ko
svchost.exe                   5436 Services                   0     5 580 Ko
svchost.exe                   5688 Services                   0     6 068 Ko
rundll32.exe                  6104 Console                    1     2 124 Ko
Microsoft.ReportingServic     6524 Services                   0    10 392 Ko
conhost.exe                   6564 Services                   0       980 Ko
fdlauncher.exe                7244 Services                   0       884 Ko
svchost.exe                   7292 Services                   0    12 932 Ko
Launchpad.exe                 7320 Services                   0     3 928 Ko
svchost.exe                   7356 Services                   0     5 188 Ko
fdhost.exe                    7388 Services                   0       912 Ko
conhost.exe                   7396 Services                   0       840 Ko
NVDisplay.Container.exe       3132 Console                    1    18 652 Ko
svchost.exe                   8436 Services                   0     6 464 Ko
dllhost.exe                   4260 Services                   0     5 356 Ko
svchost.exe                    644 Services                   0    14 112 Ko
svchost.exe                   4300 Services                   0     5 928 Ko
IAStorDataMgrSvc.exe          2052 Services                   0    41 748 Ko
SgrmBroker.exe                2884 Services                   0     3 716 Ko
svchost.exe                    112 Services                   0    12 680 Ko
svchost.exe                   5168 Services                   0     4 632 Ko
svchost.exe                   8684 Services                   0    40 344 Ko
svchost.exe                   3368 Services                   0    16 968 Ko
svchost.exe                   4928 Services                   0    14 916 Ko
nvcontainer.exe               3380 Console                    1    48 240 Ko
sihost.exe                    2828 Console                    1    34 140 Ko
svchost.exe                   1084 Console                    1    33 824 Ko
PresentationFontCache.exe     7844 Services                   0     1 888 Ko
svchost.exe                   2196 Console                    1    42 544 Ko
svchost.exe                   2820 Services                   0    16 436 Ko
svchost.exe                   2280 Services                   0     2 272 Ko
ctfmon.exe                    8868 Console                    1    10 948 Ko
igfxEM.exe                    9284 Console                    1    21 548 Ko
taskhostw.exe                 9380 Console                    1    16 772 Ko
svchost.exe                  10072 Console                    1    26 628 Ko
NVIDIA Web Helper.exe        10136 Console                    1     7 848 Ko
svchost.exe                  10172 Console                    1    32 564 Ko
conhost.exe                  10192 Console                    1     1 016 Ko
dllhost.exe                   9972 Console                    1    16 284 Ko
RuntimeBroker.exe            10548 Console                    1    18 036 Ko
RuntimeBroker.exe            11252 Console                    1    35 600 Ko
smartscreen.exe              11552 Console                    1    11 908 Ko
svchost.exe                  10828 Services                   0    12 756 Ko
SettingSyncHost.exe           9008 Console                    1     5 976 Ko
svchost.exe                   7044 Services                   0     9 264 Ko
SkypeBackgroundHost.exe      11100 Console                    1       216 Ko
SkypeApp.exe                 11892 Console                    1       616 Ko
RuntimeBroker.exe            12800 Console                    1     5 844 Ko
SecurityHealthSystray.exe    13096 Console                    1     2 700 Ko
SecurityHealthService.exe    13128 Services                   0     9 084 Ko
QASvc.exe                    13228 Services                   0     3 372 Ko
WmiPrvSE.exe                 13280 Services                   0    11 444 Ko
RtkAudUService64.exe          9392 Console                    1    11 436 Ko
QAAgent.exe                  12312 Console                    1     3 892 Ko
QAAdminAgent.exe              1840 Console                    1    13 608 Ko
igfxext.exe                  10144 Console                    1     3 208 Ko
unsecapp.exe                  2136 Console                    1     3 272 Ko
QALockHandler.exe            11464 Console                    1     3 280 Ko
unsecapp.exe                  2940 Console                    1     2 900 Ko
IAStorIcon.exe                4648 Console                    1     7 608 Ko
ApplicationFrameHost.exe      8020 Console                    1    40 032 Ko
SecurityHealthHost.exe        2312 Console                    1     4 428 Ko
ePowerButton_NB.exe          13900 Console                    1     2 692 Ko
svchost.exe                  15688 Services                   0    14 852 Ko
AcerRegistrationBackGroun     6804 Console                    1    12 740 Ko
svchost.exe                  16120 Services                   0     2 396 Ko
svchost.exe                  10212 Services                   0     3 260 Ko
RuntimeBroker.exe            16160 Console                    1    22 408 Ko
dllhost.exe                   8716 Console                    1     7 380 Ko
svchost.exe                  14988 Services                   0     4 016 Ko
svchost.exe                  14528 Services                   0     3 016 Ko
xampp-control.exe            10920 Console                    1    10 532 Ko
svchost.exe                  18332 Services                   0     5 112 Ko
svchost.exe                    848 Services                   0    13 140 Ko
CompPkgSrv.exe               19840 Console                    1     4 372 Ko
xampp-control.exe             1060 Console                    1     9 948 Ko
httpd.exe                    20916 Console                    1     1 096 Ko
conhost.exe                  16320 Console                    1     2 328 Ko
httpd.exe                    15832 Console                    1    27 652 Ko
svchost.exe                  21056 Services                   0    14 628 Ko
MsMpEng.exe                  20276 Services                   0   202 168 Ko
NisSrv.exe                   11228 Services                   0     6 920 Ko
taskhostw.exe                21740 Console                    1    12 608 Ko
xampp-control.exe            22452 Console                    1     9 772 Ko
YourPhone.exe                16144 Console                    1       908 Ko
RuntimeBroker.exe            15172 Console                    1    13 648 Ko
mysqld.exe                   11956 Console                    1    11 708 Ko
svchost.exe                  18324 Services                   0     4 196 Ko
wlanext.exe                  19364 Services                   0     1 688 Ko
conhost.exe                  19012 Services                   0       948 Ko
Discord.exe                   6128 Console                    1    66 968 Ko
Discord.exe                  11660 Console                    1    20 216 Ko
Discord.exe                  21976 Console                    1     4 544 Ko
Discord.exe                  20436 Console                    1   352 252 Ko
Discord.exe                  22332 Console                    1     9 512 Ko
WUDFHost.exe                 19692 Services                   0     1 896 Ko
HostAppServiceUpdater.exe     1480 Console                    1     8 712 Ko
AdobeUpdateService.exe       23176 Services                   0     1 884 Ko
Adobe Installer.exe          11696 Console                    1     2 416 Ko
svchost.exe                   9064 Services                   0     1 792 Ko
AdobeIPCBroker.exe            3344 Console                    1     6 092 Ko
AGSService.exe               10544 Services                   0    11 824 Ko
AGMService.exe               18664 Services                   0     4 624 Ko
unsecapp.exe                  1620 Services                   0     2 716 Ko
explorer.exe                 14840 Console                    1   169 408 Ko
StartMenuExperienceHost.e    21156 Console                    1    49 484 Ko
SearchUI.exe                 22648 Console                    1   205 660 Ko
ShellExperienceHost.exe      18236 Console                    1    73 280 Ko
Adobe Desktop Service.exe    20180 Console                    1    95 220 Ko
CCXProcess.exe               14128 Console                    1       644 Ko
node.exe                     21644 Console                    1    45 428 Ko
conhost.exe                  19304 Console                    1     1 236 Ko
CCLibrary.exe                17288 Console                    1       652 Ko
node.exe                      1804 Console                    1    25 724 Ko
conhost.exe                  18884 Console                    1     1 352 Ko
MicrosoftEdge.exe             1860 Console                    1       572 Ko
browser_broker.exe           14312 Console                    1     1 492 Ko
RuntimeBroker.exe             5460 Console                    1     1 788 Ko
MicrosoftEdgeCP.exe          16604 Console                    1       480 Ko
MicrosoftEdgeSH.exe           1664 Console                    1       268 Ko
RuntimeBroker.exe             5752 Console                    1    25 892 Ko
Creative Cloud.exe            2304 Console                    1    56 480 Ko
Adobe CEF Helper.exe         10764 Console                    1    17 804 Ko
Adobe CEF Helper.exe          1516 Console                    1   188 936 Ko
LockApp.exe                  10872 Console                    1    34 148 Ko
RuntimeBroker.exe            14744 Console                    1    20 756 Ko
CoreSync.exe                 17764 Console                    1    29 712 Ko
Adobe CEF Helper.exe         25592 Console                    1    42 164 Ko
RtkUWP.exe                    8464 Console                    1    31 628 Ko
RuntimeBroker.exe            24980 Console                    1    10 636 Ko
Teams.exe                     7048 Console                    1   110 712 Ko
Teams.exe                    24184 Console                    1    39 208 Ko
Teams.exe                    19752 Console                    1    84 876 Ko
Teams.exe                    16896 Console                    1   109 860 Ko
SystemSettings.exe           19808 Console                    1        60 Ko
Adobe CEF Helper.exe         21664 Console                    1    23 920 Ko
OneDrive.exe                 10352 Console                    1    10 300 Ko
xampp-control.exe            20412 Console                    1    18 416 Ko
chrome.exe                   10940 Console                    1   150 956 Ko
chrome.exe                   23884 Console                    1     5 996 Ko
chrome.exe                   13692 Console                    1     7 316 Ko
chrome.exe                   24620 Console                    1    39 892 Ko
chrome.exe                   20216 Console                    1    82 752 Ko
chrome.exe                    1204 Console                    1    27 700 Ko
Microsoft.Msn.News.exe       16948 Console                    1       480 Ko
RuntimeBroker.exe            24020 Console                    1    21 512 Ko
OfficeClickToRun.exe         16204 Services                   0    45 752 Ko
AppVShNotify.exe             20976 Services                   0     5 844 Ko
AppVShNotify.exe             15024 Console                    1     6 412 Ko
SearchIndexer.exe             4768 Services                   0    44 816 Ko
Discord.exe                  25352 Console                    1   129 332 Ko
Teams.exe                     9128 Console                    1    46 076 Ko
chrome.exe                   13884 Console                    1   243 848 Ko
dwm.exe                      10584 Console                    1    86 832 Ko
svchost.exe                  26184 Services                   0     4 760 Ko
MusNotifyIcon.exe            19516 Console                    1    12 580 Ko
HxOutlook.exe                24916 Console                    1        56 Ko
RuntimeBroker.exe             7100 Console                    1    18 428 Ko
HxTsr.exe                    10220 Console                    1     8 156 Ko
audiodg.exe                  22568 Services                   0    17 784 Ko
chrome.exe                   25852 Console                    1   101 456 Ko
chrome.exe                   12464 Console                    1   133 336 Ko
chrome.exe                   17964 Console                    1    16 540 Ko
Microsoft.Photos.exe         11116 Console                    1    36 764 Ko
RuntimeBroker.exe            13832 Console                    1    29 860 Ko
chrome.exe                   24920 Console                    1    37 268 Ko
chrome.exe                   10208 Console                    1   103 856 Ko
chrome.exe                    4880 Console                    1    88 084 Ko
chrome.exe                    2700 Console                    1    22 072 Ko
powershell.exe                7876 Console                    1    77 828 Ko
conhost.exe                  26076 Console                    1    16 688 Ko
svchost.exe                   3544 Services                   0     8 148 Ko
tasklist.exe                 26296 Console                    1     8 372 Ko
WmiPrvSE.exe                  4408 Services                   0     8 880 Ko
```


**svchost.exe** : Le processus svchost.exe (svchost qui signifie Service Host Process) est un processus générique de Windows qui sert d'hôte pour les autres processus et dont le fonctionnement repose sur des DLL (librairies dynamiques). Il existe ainsi autant d'entrées svchost qu'il existe de processus qui l'utilisent.

**SecurityHealthService.exe** : Le processus connu sous le nom de Windows Security Health Service appartient au logiciel Microsoft Windows Operating System de Microsoft. Il permet de protéger l'ordinateur.

**csrss.exe ** : Le processus csrss.exe (csrss signifiant Client/Server Runtime Subsystem) est un processus générique de Windows servant à gérer les fenêtres et les éléments graphiques de Windows.

**lsass.exe** : lsass.exe (Local Security Authority Subsystem) est un exécutable qui est nécessaire pour le bon fonctionnement de Windows.
Il assure l'identification des utilisateurs (utilisateurs du domaine ou utilisateurs locaux). Pour Windows 2000 et les versions postérieures, les utilisateurs du domaine sont identifiés d'après les informations de l'annuaire Active Directory. Les utilisateurs locaux sont identifiés d'après les informations de la SAM.

**unsecapp.exe** : unsecapp.exe est un fichier exécutable sur le disque dur de votre ordinateur. Il contient un code machine. Quand vous démarrez le logiciel Microsoft Windows Operating System sur votre PC, les commandes contenues dans unsecapp.exe seront exécutées sur votre PC. Dans ce but, le fichier est chargé dans la mémoire principale (RAM) et y fonctionne comme un processus Microsoft Windows Management Instrumentation

## Scripting
 
```
echo "Nom de la machine : $env:COMPUTERNAME" 
echo "Adress IP principal : "
Get-NetIPAddress -InterfaceIndex 23 | Format-Table
echo "----------------------------------------------------"
echo "OS : $env:OS" 
echo "Version de l'OS : $((Get-CimInstance Win32_OperatingSystem).version)"  
echo "Uptime : $((get-date) - $((gcim Win32_OperatingSystem)).LastBootUpTime)"
echo "Is OS up-to-date : "
echo "----------------------------------------------------"
echo "RAM : " 
echo "Utilisation : "
echo "Espace libre : $(Get-CimInstance Win32_PhysicalMemory | Measure-Object -Property capacity -Sum | Foreach {"{0:N2}" -f ([math]::round(($_.Sum / 1GB),2))})"
echo "----------------------------------------------------"
echo "Espace disque"
echo "Espace disque utilise : "
gwmi win32_logicaldisk | Format-Table DeviceId, @{n="Size";e={[math]::Round($_.Size/1GB,2)}},@{n="UsedSpace";e={[math]::Round(($_.Size-$_.FreeSpace)/1GB,2)}}
echo "Espace disque dispo : "
gwmi win32_logicaldisk | Format-Table DeviceId, @{n="Size";e={[math]::Round($_.Size/1GB,2)}},@{n="FreeSpace";e={[math]::Round($_.FreeSpace/1GB,2)}}
echo "----------------------------------------------------"
echo "Liste des Utilisateur : "
Get-LocalUser | Format-Table
echo "----------------------------------------------------"
ping 8.8.8.8
```