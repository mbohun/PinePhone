## Setting up your PinePhone in 128 EASY STEPS
![Alt text](images/thumb/Screenshot_20210713_174637_main_50pc.jpg "PinePhone")

#### `ssh`
Get the phone's IP address; on the PinePhone open
a terminal, and type:
```
[mbohun@plasma-mobile ~]$ ip -4 -o address
1: lo    inet 127.0.0.1/8 scope host lo\       valid_lft forever preferred_lft forever
2: wlan0    inet 192.168.1.105/24 brd 192.168.1.255 scope global dynamic noprefixroute wlan0\       valid_lft 85154sec preferred_lft 85154sec
```

From your PC (preferably Linux), ssh into the phone:
```
mbohun@linux-lrp0:~> ssh 192.168.1.105
mbohun@192.168.1.105's password: 
Welcome to Manjaro-ARM
~~Website: https://manjaro.org
~~Forum:   https://forum.manjaro.org/c/arm
~~Matrix:  #manjaro-arm-public:matrix.org
Last login: Mon Jul  5 20:24:47 2021 from 192.168.1.106
[mbohun@plasma-mobile ~]$
```
...and:
```
[mbohun@plasma-mobile ~]$ cat /etc/*rel*
DISTRIB_ID=Manjaro-ARM
DISTRIB_RELEASE=21.07
DISTRIB_CODENAME=
DISTRIB_DESCRIPTION="Manjaro ARM Linux"
NAME="Manjaro-ARM"
ID="manjaro-arm"
ID_LIKE="manjaro arch"
PRETTY_NAME="Manjaro ARM"
ANSI_COLOR="1;32"
HOME_URL="https://www.manjaro.org/"
SUPPORT_URL="https://forum.manjaro.org/c/arm/"
LOGO=manjarolinux
```
The PinePhone is voluntering info that it runs Manjaro (Manjaro-ARM) Linux distro.
- Manjaro Linux uses package manager: **`pacman`**
- Manjaro `pacman` wiki: [https://wiki.manjaro.org/index.php/Pacman_Overview](https://wiki.manjaro.org/index.php/Pacman_Overview)

#### `free -m`
```
[mbohun@plasma-mobile ~]$ free -m
               total        used        free      shared  buff/cache   available
Mem:            2993         718        1666         128         608        2067
Swap:           4490           0        4490
```

#### `df -hT`
```
[mbohun@plasma-mobile ~]$ df -hT
Filesystem     Type      Size  Used Avail Use% Mounted on
dev            devtmpfs  1.4G     0  1.4G   0% /dev
run            tmpfs     1.5G  1.5M  1.5G   1% /run
/dev/mmcblk2p2 ext4       29G  6.6G   21G  25% /
tmpfs          tmpfs     1.5G     0  1.5G   0% /dev/shm
tmpfs          tmpfs     1.5G   84K  1.5G   1% /tmp
/dev/mmcblk2p1 vfat      214M   39M  175M  19% /boot
tmpfs          tmpfs     300M   56K  300M   1% /run/user/1002
```
**NOTE:** The microSD card (I put in 128gb microSD) is **NOT** mounted by default. It is shown in the File browser GUI, but you have to tap on it, and mount it that way.
```
[mbohun@plasma-mobile ~]$ sudo df -hT
Filesystem     Type      Size  Used Avail Use% Mounted on
dev            devtmpfs  1.4G     0  1.4G   0% /dev
run            tmpfs     1.5G  1.5M  1.5G   1% /run
/dev/mmcblk2p2 ext4       29G  6.6G   21G  25% /
tmpfs          tmpfs     1.5G     0  1.5G   0% /dev/shm
tmpfs          tmpfs     1.5G   84K  1.5G   1% /tmp
/dev/mmcblk2p1 vfat      214M   39M  175M  19% /boot
tmpfs          tmpfs     300M   56K  300M   1% /run/user/1002
/dev/mmcblk0p1 exfat     120G  512K  120G   1% /run/media/mbohun/3966-3564
```

#### CPU
```
[mbohun@plasma-mobile ~]$ cat /proc/cpuinfo 
processor	: 0
BogoMIPS	: 48.00
Features	: fp asimd evtstrm aes pmull sha1 sha2 crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 1
BogoMIPS	: 48.00
Features	: fp asimd evtstrm aes pmull sha1 sha2 crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 2
BogoMIPS	: 48.00
Features	: fp asimd evtstrm aes pmull sha1 sha2 crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 3
BogoMIPS	: 48.00
Features	: fp asimd evtstrm aes pmull sha1 sha2 crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4
```

### First update (2021-07-05)
```
[Mon Jul  5 12:29:12 2021] Booting Linux on physical CPU 0x0000000000 [0x410fd034]
[Mon Jul  5 12:29:12 2021] Linux version 5.11.3-1-MANJARO-ARM (builduser@on2-runner) (gcc (GCC) 10.2.0, GNU ld (GNU Binutils) 2.35) #1 SMP Thu Mar 4 17:54:13 UTC 2021
[Mon Jul  5 12:29:12 2021] Machine model: Pine64 PinePhone (1.2)
...
```

#### The package manager was blocked, and it did not work:
```
# NOTE: The package manager (pacman) was blocked, and it did NOT work.
#       I had to REMOVE the pacman lock first:
#
[mbohun@plasma-mobile ~]$ sudo rm  /var/lib/pacman/db.lck
[mbohun@plasma-mobile ~]$ sudo pacman -Syu
[mbohun@plasma-mobile ~]$ sudo reboot
```

#### REBOOT
```
[mbohun@plasma-mobile ~]$ uname -a
Linux plasma-mobile 5.12.11-1-MANJARO-ARM #1 SMP Wed Jun 16 13:18:32 UTC 2021 aarch64 GNU/Linux
```
```
[Mon Jul  5 18:46:34 2021] Booting Linux on physical CPU 0x0000000000 [0x410fd034]
[Mon Jul  5 18:46:34 2021] Linux version 5.12.11-1-MANJARO-ARM (builduser@on2-runner) (gcc (GCC) 10.2.0, GNU ld (GNU Binutils) 2.35) #1 SMP Wed Jun 16 13:18:32 UTC 2021
[Mon Jul  5 18:46:34 2021] Machine model: Pine64 PinePhone (1.2)
```

### REFERENCES:
- [https://pine64.com/product/pinephone-beta-edition-with-convergence-package-linux-smartphone-open-for-preorder-soon/](https://pine64.com/product/pinephone-beta-edition-with-convergence-package-linux-smartphone-open-for-preorder-soon/)
- [https://github.com/dreemurrs-embedded/Jumpdrive](https://github.com/dreemurrs-embedded/Jumpdrive)
- TODO
