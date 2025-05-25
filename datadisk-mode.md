
## prepare installer

##### create partition
```
cfdisk /dev/sdb
```

| device    | size type |
| --------- | --------- |
| /dev/sdb1 | 3.6G      |
| /dev/sdb2 | 25G       |

##### create installer
```
cat alpine.iso > /dev/sdb1
```

## diskless installation
##### install package

```
apk add e2fsprogs cfdisk lsblk
```
##### format diskless partition

```
mkfs.ext4 -O ^has_journal,^64bit /dev/sdXY
```

*note: if /dev/sdXY does not exists please reboot*

##### create mount point

```
mkdir /media/sda2
```

##### edit fstab

```
echo "/dev/sda2 /media/sda2 ext4 noatime,ro 0 0" >> /etc/fstab
```

##### mount partition

```
mount -a
```

### install alpine linux

```
setup-alpine
```
##### keyboard layout
```
us
```
##### select variant
```
us
```
##### localhost
```
blackroz
```

##### interface
```
[eth0] 
```

##### network
```
10.10.1.21
```

##### netmask
```
255.255.255.0
```

##### gateway
```
10.10.1.1
```

##### DNS domain name
```
blackroz.srv
```

##### DNS nameserver
```
10.10.1.1
```

##### setup root password
```
toor
```

##### timezone
```
Asia/Jakarta
```

##### proxy
```
none
```

##### Network Time Protocol
```
chrony
```

##### apk mirror
```
[1] find and use fastest mirror
```

##### setup a user
```
no
```

##### ssh server
```
openssh
```

##### allow root ssh login
```
yes
```

##### enter ssh key 
```
none
```

#### disk & install
#####  wich disk would you like to use 
```
sdb
```
#####  enter where to store configs 
```
none
```
##### enter apk cache directory
```
/media/sda2/cache
```

### after install

Manually edit the lbu backups location in `/etc/lbu/lbu.conf` and configure 

```
vim /etc/lbu/lbu.conf
```

```
LBU_MEDIA=sda2
```

```
setup-apkcache /media/sda2/cache
```

```
lbu commit
```
