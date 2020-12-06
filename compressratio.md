Script started on 2020-12-06 10:18:28+00:00
]0;root@zfs:/home/vagrant[root@zfs vagrant]# lsblk
NAME                MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                   8:0    0  128G  0 disk 
├─sda1                8:1    0    1G  0 part /boot
└─sda2                8:2    0  127G  0 part 
  ├─cl_centos8-root 253:0    0   50G  0 lvm  /
  ├─cl_centos8-swap 253:1    0  2.1G  0 lvm  [SWAP]
  └─cl_centos8-home 253:2    0   75G  0 lvm  /home
sdb                   8:16   0    4G  0 disk 
sdc                   8:32   0    4G  0 disk 
sdd                   8:48   0    2G  0 disk 
sde                   8:64   0    1G  0 disk 
]0;root@zfs:/home/vagrant[root@zfs vagrant]# yum sera[K[Karch install [K[Kles zfs
Last metadata expiration check: 0:55:42 ago on Sun 06 Dec 2020 09:23:08 AM UTC.
No matches found.
]0;root@zfs:/home/vagrant[root@zfs vagrant]# exit

Script done on 2020-12-06 10:18:58+00:00
Script started on 2020-12-06 10:19:03+00:00
]0;root@zfs:/home/vagrant[root@zfs vagrant]# lsblk
NAME                MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                   8:0    0  128G  0 disk 
├─sda1                8:1    0    1G  0 part /boot
└─sda2                8:2    0  127G  0 part 
  ├─cl_centos8-root 253:0    0   50G  0 lvm  /
  ├─cl_centos8-swap 253:1    0  2.1G  0 lvm  [SWAP]
  └─cl_centos8-home 253:2    0   75G  0 lvm  /home
sdb                   8:16   0    4G  0 disk 
sdc                   8:32   0    4G  0 disk 
sdd                   8:48   0    2G  0 disk 
sde                   8:64   0    1G  0 disk 
]0;root@zfs:/home/vagrant[root@zfs vagrant]# yum list installed zfs
Installed Packages
zfs.x86_64                                 0.8.5-1.el8                                  @zfs-kmod
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zpool create poolmirror miro[Kror sdb sdc
The ZFS modules are not loaded.
Try running '/sbin/modprobe zfs' as root to load them.
]0;root@zfs:/home/vagrant[root@zfs vagrant]# /sbin/modprobe zfs
]0;root@zfs:/home/vagrant[root@zfs vagrant]# /sbin/modprobe zfszpool create poolmirror mirror sdb sdc
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs create data1/doc
cannot create 'data1/doc': no such pool 'data1'
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zpool create storaf[Kge mirror d[Ksdb sdc
/dev/sdb is in use and contains a unknown filesystem.
/dev/sdc is in use and contains a unknown filesystem.
]0;root@zfs:/home/vagrant[root@zfs vagrant]# lsblk
NAME                MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                   8:0    0  128G  0 disk 
├─sda1                8:1    0    1G  0 part /boot
└─sda2                8:2    0  127G  0 part 
  ├─cl_centos8-root 253:0    0   50G  0 lvm  /
  ├─cl_centos8-swap 253:1    0  2.1G  0 lvm  [SWAP]
  └─cl_centos8-home 253:2    0   75G  0 lvm  /home
sdb                   8:16   0    4G  0 disk 
├─sdb1                8:17   0    4G  0 part 
└─sdb9                8:25   0    8M  0 part 
sdc                   8:32   0    4G  0 disk 
├─sdc1                8:33   0    4G  0 part 
└─sdc9                8:41   0    8M  0 part 
sdd                   8:48   0    2G  0 disk 
sde                   8:64   0    1G  0 disk 
]0;root@zfs:/home/vagrant[root@zfs vagrant]# lsblkzpool create storage mirror sdb sdc
[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[15Pfs create data1/doc[K[K[K[K[K[K[K[K[Kstorage/mydir
cannot create 'storage/mydir': no such pool 'storage'
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs create storage/mydir[1P/mydir[1P/mydir[1P/mydir[1P/mydir[1P/mydir[1P/mydir[1P/mydirm/mydiri/mydirr/mydirr/mydiro/mydirr/mydir
cannot create 'mirror/mydir': no such pool 'mirror'
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs -h
unrecognized command '-h'
usage: zfs command args ...
where 'command' is one of the following:

	version

	create [-p] [-o property=value] ... <filesystem>
	create [-ps] [-b blocksize] [-o property=value] ... -V <size> <volume>
	destroy [-fnpRrv] <filesystem|volume>
	destroy [-dnpRrv] <filesystem|volume>@<snap>[%<snap>][,...]
	destroy <filesystem|volume>#<bookmark>

	snapshot [-r] [-o property=value] ... <filesystem|volume>@<snap> ...
	rollback [-rRf] <snapshot>
	clone [-p] [-o property=value] ... <snapshot> <filesystem|volume>
	promote <clone-filesystem>
	rename [-f] <filesystem|volume|snapshot> <filesystem|volume|snapshot>
	rename [-f] -p <filesystem|volume> <filesystem|volume>
	rename -r <snapshot> <snapshot>
	bookmark <snapshot> <bookmark>
	program [-jn] [-t <instruction limit>] [-m <memory limit (b)>]
	    <pool> <program file> [lua args...]

	list [-Hp] [-r|-d max] [-o property[,...]] [-s property]...
	    [-S property]... [-t type[,...]] [filesystem|volume|snapshot] ...

	set <property=value> ... <filesystem|volume|snapshot> ...
	get [-rHp] [-d max] [-o "all" | field[,...]]
	    [-t type[,...]] [-s source[,...]]
	    <"all" | property[,...]> [filesystem|volume|snapshot|bookmark] ...
	inherit [-rS] <property> <filesystem|volume|snapshot> ...
	upgrade [-v]
	upgrade [-r] [-V version] <-a | filesystem ...>

	userspace [-Hinp] [-o field[,...]] [-s field] ...
	    [-S field] ... [-t type[,...]] <filesystem|snapshot>
	groupspace [-Hinp] [-o field[,...]] [-s field] ...
	    [-S field] ... [-t type[,...]] <filesystem|snapshot>
	projectspace [-Hp] [-o field[,...]] [-s field] ... 
	    [-S field] ... <filesystem|snapshot>

	project [-d|-r] <directory|file ...>
	project -c [-0] [-d|-r] [-p id] <directory|file ...>
	project -C [-k] [-r] <directory ...>
	project [-p id] [-r] [-s] <directory ...>

	mount
	mount [-lvO] [-o opts] <-a | filesystem>
	unmount [-f] <-a | filesystem|mountpoint>
	share [-l] <-a [nfs|smb] | filesystem>
	unshare <-a [nfs|smb] | filesystem|mountpoint>

	send [-DnPpRvLecwhb] [-[i|I] snapshot] <snapshot>
	send [-nvPLecw] [-i snapshot|bookmark] <filesystem|volume|snapshot>
	send [-nvPe] -t <receive_resume_token>
	receive [-vnsFhu] [-o <property>=<value>] ... [-x <property>] ...
	    <filesystem|volume|snapshot>
	receive [-vnsFhu] [-o <property>=<value>] ... [-x <property>] ... 
	    [-d | -e] <filesystem>
	receive -A <filesystem|volume>

	allow <filesystem|volume>
	allow [-ldug] <"everyone"|user|group>[,...] <perm|@setname>[,...]
	    <filesystem|volume>
	allow [-ld] -e <perm|@setname>[,...] <filesystem|volume>
	allow -c <perm|@setname>[,...] <filesystem|volume>
	allow -s @setname <perm|@setname>[,...] <filesystem|volume>

	unallow [-rldug] <"everyone"|user|group>[,...]
	    [<perm|@setname>[,...]] <filesystem|volume>
	unallow [-rld] -e [<perm|@setname>[,...]] <filesystem|volume>
	unallow [-r] -c [<perm|@setname>[,...]] <filesystem|volume>
	unallow [-r] -s @setname [<perm|@setname>[,...]] <filesystem|volume>

	hold [-r] <tag> <snapshot> ...
	holds [-rH] <snapshot> ...
	release [-r] <tag> <snapshot> ...
	diff [-FHt] <snapshot> [snapshot|filesystem]

	load-key [-rn] [-L <keylocation>] <-a | filesystem|volume>
	unload-key [-r] <-a | filesystem|volume>
	change-key [-l] [-o keyformat=<value>]
	    [-o keylocation=<value>] [-o pbkfd2iters=<value>]
	    <filesystem|volume>
	change-key -i [-l] <filesystem|volume>

Each dataset is of the form: pool/[dataset/]*dataset[@name]

For the property list, run: zfs set|get

For the delegated permission list, run: zfs allow|unallow
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs list
NAME         USED  AVAIL     REFER  MOUNTPOINT
poolmirror  91.5K  3.62G       24K  /poolmirror
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs list[2P-hcreate mirror/mydir[1P/mydir[1P/mydir[1P/mydir[1P/mydir[1P/mydir[1P/mydirp/mydiro/mydiro/mydirl/mydirm/mydiri/mydirr/mydirr/mydiro/mydirr/mydir
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs create poolmirror/mydir[K[K[K[K[Kdata/doc
cannot create 'poolmirror/data/doc': parent does not exist
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs create poolmirror/data/doc[K[K[K
cannot create 'poolmirror/data/': trailing slash in name
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs create poolmirror/data/[K
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs create poolmirror/data/doc
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs create poolmirror/data/doc[K/doc[3Pmydirlist[K
NAME                  USED  AVAIL     REFER  MOUNTPOINT
poolmirror            178K  3.62G       27K  /poolmirror
poolmirror/data        48K  3.62G       24K  /poolmirror/data
poolmirror/data/doc    24K  3.62G       24K  /poolmirror/data/doc
poolmirror/mydir       24K  3.62G       24K  /poolmirror/mydir
]0;root@zfs:/home/vagrant[root@zfs vagrant]# mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=1434476k,nr_inodes=358619,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,seclabel,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime,seclabel)
bpf on /sys/fs/bpf type bpf (rw,nosuid,nodev,noexec,relatime,mode=700)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,freezer)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,devices)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,perf_event)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpuset)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,rdma)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,pids)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,net_cls,net_prio)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpu,cpuacct)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,hugetlb)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,memory)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,blkio)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/mapper/cl_centos8-root on / type xfs (rw,relatime,seclabel,attr2,inode64,noquota)
selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=39,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=18007)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel,pagesize=2M)
debugfs on /sys/kernel/debug type debugfs (rw,relatime,seclabel)
/dev/mapper/cl_centos8-home on /home type xfs (rw,relatime,seclabel,attr2,inode64,noquota)
/dev/sda1 on /boot type ext4 (rw,relatime,seclabel)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=290284k,mode=700,uid=1000,gid=1000)
poolmirror on /poolmirror type zfs (rw,seclabel,xattr,noacl)
poolmirror/mydir on /poolmirror/mydir type zfs (rw,seclabel,xattr,noacl)
poolmirror/data on /poolmirror/data type zfs (rw,seclabel,xattr,noacl)
poolmirror/data/doc on /poolmirror/data/doc type zfs (rw,seclabel,xattr,noacl)
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs get mounted
NAME                 PROPERTY  VALUE    SOURCE
poolmirror           mounted   yes      -
poolmirror/data      mounted   yes      -
poolmirror/data/doc  mounted   yes      -
poolmirror/mydir     mounted   yes      -
]0;root@zfs:/home/vagrant[root@zfs vagrant]# df -hT
Filesystem                  Type      Size  Used Avail Use% Mounted on
devtmpfs                    devtmpfs  1.4G     0  1.4G   0% /dev
tmpfs                       tmpfs     1.4G     0  1.4G   0% /dev/shm
tmpfs                       tmpfs     1.4G  8.5M  1.4G   1% /run
tmpfs                       tmpfs     1.4G     0  1.4G   0% /sys/fs/cgroup
/dev/mapper/cl_centos8-root xfs        50G  2.1G   48G   5% /
/dev/mapper/cl_centos8-home xfs        75G  568M   75G   1% /home
/dev/sda1                   ext4      976M  140M  770M  16% /boot
tmpfs                       tmpfs     284M     0  284M   0% /run/user/1000
poolmirror                  zfs       3.7G  128K  3.7G   1% /poolmirror
poolmirror/mydir            zfs       3.7G  128K  3.7G   1% /poolmirror/mydir
poolmirror/data             zfs       3.7G  128K  3.7G   1% /poolmirror/data
poolmirror/data/doc         zfs       3.7G  128K  3.7G   1% /poolmirror/data/doc
]0;root@zfs:/home/vagrant[root@zfs vagrant]# df -hTzfs get mounted[10Pmountzfs listcreate poolmirror/data/doc/compressed1
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs create poolmirror/data/doc/compressed1[K2
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs create poolmirror/data/doc/compressed2[K3
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs create poolmirror/data/doc/compressed3[K4
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs create poolmirror/data/doc/compressed4[K5
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs ger[Kt mounted
NAME                             PROPERTY  VALUE    SOURCE
poolmirror                       mounted   yes      -
poolmirror/data                  mounted   yes      -
poolmirror/data/doc              mounted   yes      -
poolmirror/data/doc/compressed1  mounted   yes      -
poolmirror/data/doc/compressed2  mounted   yes      -
poolmirror/data/doc/compressed3  mounted   yes      -
poolmirror/data/doc/compressed4  mounted   yes      -
poolmirror/data/doc/compressed5  mounted   yes      -
poolmirror/mydir                 mounted   yes      -
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs set compress=gzip poolmirror/data/doc/compressed1
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs set compress=gzip poolmirror/data/doc/compressed1[1P poolmirror/data/doc/compressed1[1P poolmirror/data/doc/compressed1[1P poolmirror/data/doc/compressed1[1P poolmirror/data/doc/compressed1g poolmirror/data/doc/compressed1z poolmirror/data/doc/compressed1i poolmirror/data/doc/compressed1p poolmirror/data/doc/compressed1- poolmirror/data/doc/compressed19 poolmirror/data/doc/compressed1[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[K2
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs set compress=gzip-9 poolmirror/data/doc/compressed2[K3[C[C[1P poolmirror/data/doc/compressed3[1P poolmirror/data/doc/compressed3[1P poolmirror/data/doc/compressed3[1P poolmirror/data/doc/compressed3[1P poolmirror/data/doc/compressed3[1P poolmirror/data/doc/compressed3l poolmirror/data/doc/compressed3z poolmirror/data/doc/compressed34 poolmirror/data/doc/compressed3
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs set compress=lz4 poolmirror/data/doc/compressed3[K4[1P poolmirror/data/doc/compressed4j poolmirror/data/doc/compressed4b poolmirror/data/doc/compressed4
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs set compress=lzjb poolmirror/data/doc/compressed4[K5[1P poolmirror/data/doc/compressed5[1P poolmirror/data/doc/compressed5[1P poolmirror/data/doc/compressed5[1P poolmirror/data/doc/compressed5z poolmirror/data/doc/compressed5l poolmirror/data/doc/compressed5e poolmirror/data/doc/compressed5
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs get all | grep compressration[K
poolmirror                       [01;31m[Kcompressratio[m[K         1.00x                             -
poolmirror                       ref[01;31m[Kcompressratio[m[K      1.00x                             -
poolmirror/data                  [01;31m[Kcompressratio[m[K         1.00x                             -
poolmirror/data                  ref[01;31m[Kcompressratio[m[K      1.00x                             -
poolmirror/data/doc              [01;31m[Kcompressratio[m[K         1.00x                             -
poolmirror/data/doc              ref[01;31m[Kcompressratio[m[K      1.00x                             -
poolmirror/data/doc/compressed1  [01;31m[Kcompressratio[m[K         1.00x                             -
poolmirror/data/doc/compressed1  ref[01;31m[Kcompressratio[m[K      1.00x                             -
poolmirror/data/doc/compressed2  [01;31m[Kcompressratio[m[K         1.00x                             -
poolmirror/data/doc/compressed2  ref[01;31m[Kcompressratio[m[K      1.00x                             -
poolmirror/data/doc/compressed3  [01;31m[Kcompressratio[m[K         1.00x                             -
poolmirror/data/doc/compressed3  ref[01;31m[Kcompressratio[m[K      1.00x                             -
poolmirror/data/doc/compressed4  [01;31m[Kcompressratio[m[K         1.00x                             -
poolmirror/data/doc/compressed4  ref[01;31m[Kcompressratio[m[K      1.00x                             -
poolmirror/data/doc/compressed5  [01;31m[Kcompressratio[m[K         1.00x                             -
poolmirror/data/doc/compressed5  ref[01;31m[Kcompressratio[m[K      1.00x                             -
poolmirror/mydir                 [01;31m[Kcompressratio[m[K         1.00x                             -
poolmirror/mydir                 ref[01;31m[Kcompressratio[m[K      1.00x                             -
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs get all | grep compressratio[K[K[Kcompression
NAME                             PROPERTY     VALUE     SOURCE
poolmirror                       compression  off       default
poolmirror/data                  compression  off       default
poolmirror/data/doc              compression  off       default
poolmirror/data/doc/compressed1  compression  gzip      local
poolmirror/data/doc/compressed2  compression  gzip-9    local
poolmirror/data/doc/compressed3  compression  lz4       local
poolmirror/data/doc/compressed4  compression  lzjb      local
poolmirror/data/doc/compressed5  compression  zle       local
poolmirror/mydir                 compression  off       default
]0;root@zfs:/home/vagrant[root@zfs vagrant]# wget -O War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[1@/[1@p[1@o[1@olmirror/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt
t.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CdWar_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CaWar_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CtWar_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CaWar_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CdWar_and_Peace.txt http://www.gutenberg.org/ebooks/26[C0.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CoWar_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cc/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CcWar_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CoWar_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CmpressedWar_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C1War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C


--2020-12-06 10:39:14--  http://www.gutenberg.org/ebooks/2600.txt.utf-8
Resolving www.gutenberg.org (www.gutenberg.org)... 152.19.134.47, 2610:28:3090:3000:0:bad:cafe:47
Connecting to www.gutenberg.org (www.gutenberg.org)|152.19.134.47|:80... connected.
HTTP request sent, awaiting response... 302 Found
Location: http://www.gutenberg.org/cache/epub/2600/pg2600.txt [following]
--2020-12-06 10:39:15--  http://www.gutenberg.org/cache/epub/2600/pg2600.txt
Reusing existing connection to www.gutenberg.org:80.
HTTP request sent, awaiting response... 406 Not Acceptable
2020-12-06 10:39:16 ERROR 406: Not Acceptable.

]0;root@zfs:/home/vagrant[root@zfs vagrant]# wget -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenber
rg.org/ebooks/2600.txt.utf-8
[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A-d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/
/2600.txt.utf-8[A


Setting --user-agent (useragent) to Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0
Setting --user-agent (useragent) to Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0
Setting --output-document (outputdocument) to /poolmirror/data/doc/compressed1/War_and_Peace.txt
Setting --output-document (outputdocument) to /poolmirror/data/doc/compressed1/War_and_Peace.txt
DEBUG output created by Wget 1.19.5 on linux-gnu.

Reading HSTS entries from /root/.wget-hsts
URI encoding = ‘UTF-8’
--2020-12-06 10:43:16--  http://www.gutenberg.org/ebooks/2600.txt.utf-8
Resolving www.gutenberg.org (www.gutenberg.org)... 152.19.134.47, 2610:28:3090:3000:0:bad:cafe:47
Caching www.gutenberg.org => 152.19.134.47 2610:28:3090:3000:0:bad:cafe:47
Connecting to www.gutenberg.org (www.gutenberg.org)|152.19.134.47|:80... connected.
Created socket 4.
Releasing 0x0000557157cace10 (new refcount 1).

---request begin---
GET /ebooks/2600.txt.utf-8 HTTP/1.1

User-Agent: Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0

Accept: */*

Accept-Encoding: identity

Host: www.gutenberg.org

Connection: Keep-Alive



---request end---
HTTP request sent, awaiting response... 
---response begin---
HTTP/1.1 302 Found

Date: Sun, 06 Dec 2020 10:43:17 GMT

Server: Apache

Location: http://www.gutenberg.org/cache/epub/2600/pg2600.txt

Content-Length: 302

Content-Type: text/html; charset=iso-8859-1



---response end---
302 Found
Registered socket 4 for persistent reuse.
URI content encoding = ‘iso-8859-1’
Location: http://www.gutenberg.org/cache/epub/2600/pg2600.txt [following]
Skipping 302 bytes of body: [<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>302 Found</title>
</head><body>
<h1>Found</h1>
<p>The document has moved <a href="http://www.gutenberg.org/cache/epub/2600/pg2600.txt">here</a>.</p>
<hr>
<address>Apache Server at www.gutenberg.org Port 80</address>
</body></html>
] done.
URI content encoding = None
--2020-12-06 10:43:17--  http://www.gutenberg.org/cache/epub/2600/pg2600.txt
Reusing existing connection to www.gutenberg.org:80.
Reusing fd 4.

---request begin---
GET /cache/epub/2600/pg2600.txt HTTP/1.1

User-Agent: Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0

Accept: */*

Accept-Encoding: identity

Host: www.gutenberg.org

Connection: Keep-Alive



---request end---
HTTP request sent, awaiting response... 
---response begin---
HTTP/1.1 406 Not Acceptable

Date: Sun, 06 Dec 2020 10:43:17 GMT

Server: Apache

Alternates: {"pg2600.txt.utf8.gzip" 1 {type text/plain} {charset utf-8} {encoding gzip} {length 1209374}}

Vary: negotiate

TCN: list

Content-Length: 488

Content-Type: text/html; charset=iso-8859-1



---response end---
406 Not Acceptable
URI content encoding = ‘iso-8859-1’
Skipping 488 bytes of body: [<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>406 Not Acceptable</title>
</head><body>
<h1>Not Acceptable</h1>
<p>An appropriate representation of the requested resource /cache/epub/2600/pg2600.txt could not be found on this server.</p>
Available variants:
<ul>
<li><a href="pg2600.txt.utf8.gzip">pg2600.txt.utf8.gzip</a> , type text/plain, charset utf-8, encoding gzip</li>
</ul>
<hr>
<address>Apache Server at www.gutenberg.org Port 80</address>
</body></html>
] done.
2020-12-06 10:43:17 ERROR 406: Not Acceptable.

]0;root@zfs:/home/vagrant[root@zfs vagrant]# wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Fir
refox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/
/2600.txt.utf-8
Setting --user-agent (useragent) to Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0
Setting --user-agent (useragent) to Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0
Setting --output-document (outputdocument) to /poolmirror/data/doc/compressed1/War_and_Peace.txt
Setting --output-document (outputdocument) to /poolmirror/data/doc/compressed1/War_and_Peace.txt
DEBUG output created by Wget 1.19.5 on linux-gnu.

Reading HSTS entries from /root/.wget-hsts
URI encoding = ‘UTF-8’
--2020-12-06 10:45:55--  http://www.gutenberg.org/ebooks/2600.txt.utf-8
Resolving www.gutenberg.org (www.gutenberg.org)... 152.19.134.47, 2610:28:3090:3000:0:bad:cafe:47
Caching www.gutenberg.org => 152.19.134.47 2610:28:3090:3000:0:bad:cafe:47
Connecting to www.gutenberg.org (www.gutenberg.org)|152.19.134.47|:80... connected.
Created socket 4.
Releasing 0x0000557ffacefe10 (new refcount 1).

---request begin---
GET /ebooks/2600.txt.utf-8 HTTP/1.1

User-Agent: Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0

Accept: */*

Accept-Encoding: identity

Host: www.gutenberg.org

Connection: Keep-Alive



---request end---
HTTP request sent, awaiting response... 
---response begin---
HTTP/1.1 302 Found

Date: Sun, 06 Dec 2020 10:45:55 GMT

Server: Apache

Location: http://www.gutenberg.org/cache/epub/2600/pg2600.txt

Content-Length: 302

Content-Type: text/html; charset=iso-8859-1



---response end---
302 Found
Registered socket 4 for persistent reuse.
URI content encoding = ‘iso-8859-1’
Location: http://www.gutenberg.org/cache/epub/2600/pg2600.txt [following]
Skipping 302 bytes of body: [<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>302 Found</title>
</head><body>
<h1>Found</h1>
<p>The document has moved <a href="http://www.gutenberg.org/cache/epub/2600/pg2600.txt">here</a>.</p>
<hr>
<address>Apache Server at www.gutenberg.org Port 80</address>
</body></html>
] done.
URI content encoding = None
--2020-12-06 10:45:56--  http://www.gutenberg.org/cache/epub/2600/pg2600.txt
Reusing existing connection to www.gutenberg.org:80.
Reusing fd 4.

---request begin---
GET /cache/epub/2600/pg2600.txt HTTP/1.1

User-Agent: Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0

Accept: */*

Accept-Encoding: identity

Host: www.gutenberg.org

Connection: Keep-Alive



---request end---
HTTP request sent, awaiting response... 
---response begin---
HTTP/1.1 406 Not Acceptable

Date: Sun, 06 Dec 2020 10:45:56 GMT

Server: Apache

Alternates: {"pg2600.txt.utf8.gzip" 1 {type text/plain} {charset utf-8} {encoding gzip} {length 1209374}}

Vary: negotiate

TCN: list

Content-Length: 488

Content-Type: text/html; charset=iso-8859-1



---response end---
406 Not Acceptable
URI content encoding = ‘iso-8859-1’
Skipping 488 bytes of body: [<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>406 Not Acceptable</title>
</head><body>
<h1>Not Acceptable</h1>
<p>An appropriate representation of the requested resource /cache/epub/2600/pg2600.txt could not be found on this server.</p>
Available variants:
<ul>
<li><a href="pg2600.txt.utf8.gzip">pg2600.txt.utf8.gzip</a> , type text/plain, charset utf-8, encoding gzip</li>
</ul>
<hr>
<address>Apache Server at www.gutenberg.org Port 80</address>
</body></html>
] done.
2020-12-06 10:45:56 ERROR 406: Not Acceptable.

]0;root@zfs:/home/vagrant[root@zfs vagrant]# wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Fir
refox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/
/2600.txt.utf-8
[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C
[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CMozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2[1P600.txt.utf-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/26[1P00.txt.utf-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Czilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/260[C[1P.txt.utf-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600[1P.txt.utf-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Clla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.[1Ptxt.utf-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Ca/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.t[1Pxt.utf-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Ca/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.tx[1Pt.utf-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt[1P.utf-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.[1Putf-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.u[1Ptf-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.ut[1Pf-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf[1P-8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C(Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-[1P8[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CWindows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[K[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cindows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8 
[K[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cndows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /p[1P

[K[A[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cdows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /po[C[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poo[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cws NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /pool[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cs NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolm[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmi[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CNT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmir[C[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirr[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C x.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirro[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cx.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C.y; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cy; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/d[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C; rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/da[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C rv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/dat[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Crv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cv:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C:10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/d[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C10.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/do[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C0.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C.0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C0) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/c[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C) Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/co[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C Gecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/com[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CGecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/comp[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cecko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compr[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Ccko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compre[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cko/20100101 Firefox/10.0" -O /poolmirror/data/doc/compres[C[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Co/20100101 Firefox/10.0" -O /poolmirror/data/doc/compress[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C/20100101 Firefox/10.0" -O /poolmirror/data/doc/compresse[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C20100101 Firefox/10.0" -O /poolmirror/data/doc/compressed[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C0100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C100101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C00101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/W[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/Wa[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C101 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C01 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C1 Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_a[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C Firefox/10.0" -O /poolmirror/data/doc/compressed1/War_an[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[CFirefox/10.0" -O /poolmirror/data/doc/compressed1/War_and[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cirefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Crefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_P[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cefox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Pe[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cfox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Pea[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cox/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peac[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cx/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C/10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C10.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.t[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C0.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.tx[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C.0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt[1P http://www.gutenberg.org/ebooks/2600.txt.utf-8[A0" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt [1Phttp://www.gutenberg.org/ebooks/2600.txt.utf-8[A" -O /poolmirror/data/doc/compressed1/War_and_Peace.txt h[1Pttp://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt ht[C[1Pp://www.gutenberg.org/ebooks/2600.txt.utf-8[AA -O /poolmirror/data/doc/compressed1/War_and_Peace.txt h[Ctp://www.gutenberg.org/ebooks/2600.txt.utf-8[AG -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[AE -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[AN -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[AT -O /poolmirror/data/doc/compressed1/War_and_Peace.t[1@x[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C


Setting --user-agent (useragent) to AGENT
Setting --user-agent (useragent) to AGENT
Setting --output-document (outputdocument) to /poolmirror/data/doc/compressed1/War_and_Peace.txt
Setting --output-document (outputdocument) to /poolmirror/data/doc/compressed1/War_and_Peace.txt
DEBUG output created by Wget 1.19.5 on linux-gnu.

Reading HSTS entries from /root/.wget-hsts
URI encoding = ‘UTF-8’
--2020-12-06 10:46:45--  http://www.gutenberg.org/ebooks/2600.txt.utf-8
Resolving www.gutenberg.org (www.gutenberg.org)... 152.19.134.47, 2610:28:3090:3000:0:bad:cafe:47
Caching www.gutenberg.org => 152.19.134.47 2610:28:3090:3000:0:bad:cafe:47
Connecting to www.gutenberg.org (www.gutenberg.org)|152.19.134.47|:80... connected.
Created socket 4.
Releasing 0x0000561164340d90 (new refcount 1).

---request begin---
GET /ebooks/2600.txt.utf-8 HTTP/1.1

User-Agent: AGENT

Accept: */*

Accept-Encoding: identity

Host: www.gutenberg.org

Connection: Keep-Alive



---request end---
HTTP request sent, awaiting response... 
---response begin---
HTTP/1.1 302 Found

Date: Sun, 06 Dec 2020 10:46:45 GMT

Server: Apache

Location: http://www.gutenberg.org/cache/epub/2600/pg2600.txt

Content-Length: 302

Content-Type: text/html; charset=iso-8859-1



---response end---
302 Found
Registered socket 4 for persistent reuse.
URI content encoding = ‘iso-8859-1’
Location: http://www.gutenberg.org/cache/epub/2600/pg2600.txt [following]
Skipping 302 bytes of body: [<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>302 Found</title>
</head><body>
<h1>Found</h1>
<p>The document has moved <a href="http://www.gutenberg.org/cache/epub/2600/pg2600.txt">here</a>.</p>
<hr>
<address>Apache Server at www.gutenberg.org Port 80</address>
</body></html>
] done.
URI content encoding = None
--2020-12-06 10:46:45--  http://www.gutenberg.org/cache/epub/2600/pg2600.txt
Reusing existing connection to www.gutenberg.org:80.
Reusing fd 4.

---request begin---
GET /cache/epub/2600/pg2600.txt HTTP/1.1

User-Agent: AGENT

Accept: */*

Accept-Encoding: identity

Host: www.gutenberg.org

Connection: Keep-Alive



---request end---
HTTP request sent, awaiting response... 
---response begin---
HTTP/1.1 406 Not Acceptable

Date: Sun, 06 Dec 2020 10:46:46 GMT

Server: Apache

Alternates: {"pg2600.txt.utf8.gzip" 1 {type text/plain} {charset utf-8} {encoding gzip} {length 1209374}}

Vary: negotiate

TCN: list

Content-Length: 488

Content-Type: text/html; charset=iso-8859-1



---response end---
406 Not Acceptable
URI content encoding = ‘iso-8859-1’
Skipping 488 bytes of body: [<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>406 Not Acceptable</title>
</head><body>
<h1>Not Acceptable</h1>
<p>An appropriate representation of the requested resource /cache/epub/2600/pg2600.txt could not be found on this server.</p>
Available variants:
<ul>
<li><a href="pg2600.txt.utf8.gzip">pg2600.txt.utf8.gzip</a> , type text/plain, charset utf-8, encoding gzip</li>
</ul>
<hr>
<address>Apache Server at www.gutenberg.org Port 80</address>
</body></html>
] done.
2020-12-06 10:46:46 ERROR 406: Not Acceptable.

]0;root@zfs:/home/vagrant[root@zfs vagrant]# wget -d --user-agent=AGENT -O /poolmirror/data/doc/compressed1/War_and_Peace.t
txt http://www.gutenberg.org/ebooks/2600.txt.utf-8
[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C -O /poolmirror/data/doc/compressed1/War_and_Peace.tx[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C -O /poolmirror/data/doc/compressed1/War_and_Peace.txt[1P http://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt [1Phttp://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt h[1Pttp://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt ht[C[1Pp://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt htt[1Pp://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http[1P://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http:[1P//www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http:/[C[1Pwww.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://[1Pwww.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://w[C[C[1P.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://ww[C[1P.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www[1P.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.[1Pgutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.g[1Putenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gu[1Ptenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gut[1Penberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gute[1Pnberg.org/ebooks/2600.txt.utf-8[A-O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.guten[1Pberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenb[1Perg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenbe[1Prg.org/ebooks/2600.txt.utf-8[A- -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[AU -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A


/poolmirror/data/doc/compressed1/War_and_Peace.txt: Scheme missing.
--2020-12-06 10:47:00--  http://www.gutenberg.org/ebooks/2600.txt.utf-8
Resolving www.gutenberg.org (www.gutenberg.org)... 152.19.134.47, 2610:28:3090:3000:0:bad:cafe:47
Connecting to www.gutenberg.org (www.gutenberg.org)|152.19.134.47|:80... connected.
HTTP request sent, awaiting response... 302 Found
Location: http://www.gutenberg.org/cache/epub/2600/pg2600.txt [following]
--2020-12-06 10:47:00--  http://www.gutenberg.org/cache/epub/2600/pg2600.txt
Reusing existing connection to www.gutenberg.org:80.
HTTP request sent, awaiting response... 406 Not Acceptable
2020-12-06 10:47:01 ERROR 406: Not Acceptable.

]0;root@zfs:/home/vagrant[root@zfs vagrant]# wget -U -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.guten
nberg.org/ebooks/2600.txt.utf-8
[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenb[1Perg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenbe[1Prg.org/ebooks/2600.txt.utf-8[Aerror 406 not acceptable. -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peac[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C -O /poolmirror/data/doc/compressed1/War_and_Peace[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C -O /poolmirror/data/doc/compressed1/War_and_Peace.[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C -O /poolmirror/data/doc/compressed1/War_and_Peace.t[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C -O /poolmirror/data/doc/compressed1/War_and_Peace.tx[1P[A[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C -O /poolmirror/data/doc/compressed1/War_and_Peace.txt[1P http://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt [1Phttp://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt h[1Pttp://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt ht[C[1Pp://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt htt[1Pp://www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http[1P://www.gutenberg.org/ebooks/2600.txt.utf-8[A-O /poolmirror/data/doc/compressed1/War_and_Peace.txt http:[1P//www.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http:/[C[1Pwww.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://[1Pwww.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://w[C[C[1P.gutenberg.org/ebooks/2600.txt.utf-8[A-O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://ww[C[1P.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www[1P.gutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.[1Pgutenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.g[1Putenberg.org/ebooks/2600.txt.utf-8[A-O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gu[1Ptenberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gut[1Penberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gute[1Pnberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.guten[1Pberg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenb[1Perg.org/ebooks/2600.txt.utf-8[A -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenbe[1Prg.org/ebooks/2600.txt.utf-8[A--no-check-certificate -O /poolmirror/data/doc/compressed1/War_and_Peace.txt http://www.gutenberg.org/ebooks/2600.txt.utf-8[A


--2020-12-06 10:52:41--  http://www.gutenberg.org/ebooks/2600.txt.utf-8
Resolving www.gutenberg.org (www.gutenberg.org)... 152.19.134.47, 2610:28:3090:3000:0:bad:cafe:47
Connecting to www.gutenberg.org (www.gutenberg.org)|152.19.134.47|:80... connected.
HTTP request sent, awaiting response... 302 Found
Location: http://www.gutenberg.org/cache/epub/2600/pg2600.txt [following]
--2020-12-06 10:52:41--  http://www.gutenberg.org/cache/epub/2600/pg2600.txt
Reusing existing connection to www.gutenberg.org:80.
HTTP request sent, awaiting response... 406 Not Acceptable
2020-12-06 10:52:42 ERROR 406: Not Acceptable.

]0;root@zfs:/home/vagrant[root@zfs vagrant]# [H[2J[root@zfs vagrant]# cp pg2600.txt /m[Kpoolmirror/
data/  mydir/ 
[root@zfs vagrant]# cp pg2600.txt /poolmirror/data/doc/compressed1
]0;root@zfs:/home/vagrant[root@zfs vagrant]# cp pg2600.txt /poolmirror/data/doc/compressed1[K2
]0;root@zfs:/home/vagrant[root@zfs vagrant]# cp pg2600.txt /poolmirror/data/doc/compressed2[K3
]0;root@zfs:/home/vagrant[root@zfs vagrant]# cp pg2600.txt /poolmirror/data/doc/compressed3[K4
]0;root@zfs:/home/vagrant[root@zfs vagrant]# cp pg2600.txt /poolmirror/data/doc/compressed4[K5
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs get compressiuon[K[K[Kon.[K, compression [Kratio
cannot open 'compressionratio': dataset does not exist
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs get compression, compressionratio[C[C[1Pcompressionratio
bad property list: invalid property 'compressionratio'
usage:
	get [-rHp] [-d max] [-o "all" | field[,...]]
	    [-t type[,...]] [-s source[,...]]
	    <"all" | property[,...]> [filesystem|volume|snapshot|bookmark] ...

The following properties are supported:

	PROPERTY       EDIT  INHERIT   VALUES

	available        NO       NO   <size>
	clones           NO       NO   <dataset>[,...]
	compressratio    NO       NO   <1.00x or higher if compressed>
	createtxg        NO       NO   <uint64>
	creation         NO       NO   <date>
	defer_destroy    NO       NO   yes | no
	encryptionroot   NO       NO   <filesystem | volume>
	filesystem_count  NO       NO   <count>
	guid             NO       NO   <uint64>
	keystatus        NO       NO   none | unavailable | available
	logicalreferenced  NO       NO   <size>
	logicalused      NO       NO   <size>
	mounted          NO       NO   yes | no
	objsetid         NO       NO   <uint64>
	origin           NO       NO   <snapshot>
	receive_resume_token  NO       NO   <string token>
	refcompressratio  NO       NO   <1.00x or higher if compressed>
	referenced       NO       NO   <size>
	snapshot_count   NO       NO   <count>
	type             NO       NO   filesystem | volume | snapshot | bookmark
	used             NO       NO   <size>
	usedbychildren   NO       NO   <size>
	usedbydataset    NO       NO   <size>
	usedbyrefreservation  NO       NO   <size>
	usedbysnapshots  NO       NO   <size>
	userrefs         NO       NO   <count>
	written          NO       NO   <size>
	aclinherit      YES      YES   discard | noallow | restricted | passthrough | passthrough-x
	acltype         YES      YES   noacl | posixacl
	atime           YES      YES   on | off
	canmount        YES       NO   on | off | noauto
	casesensitivity  NO      YES   sensitive | insensitive | mixed
	checksum        YES      YES   on | off | fletcher2 | fletcher4 | sha256 | sha512 | skein | edonr
	compression     YES      YES   on | off | lzjb | gzip | gzip-[1-9] | zle | lz4
	context         YES       NO   <selinux context>
	copies          YES      YES   1 | 2 | 3
	dedup           YES      YES   on | off | verify | sha256[,verify], sha512[,verify], skein[,verify], edonr,verify
	defcontext      YES       NO   <selinux defcontext>
	devices         YES      YES   on | off
	dnodesize       YES      YES   legacy | auto | 1k | 2k | 4k | 8k | 16k
	encryption       NO      YES   on | off | aes-128-ccm | aes-192-ccm | aes-256-ccm | aes-128-gcm | aes-192-gcm | aes-256-gcm
	exec            YES      YES   on | off
	filesystem_limit YES       NO   <count> | none
	fscontext       YES       NO   <selinux fscontext>
	keyformat        NO       NO   none | raw | hex | passphrase
	keylocation     YES       NO   prompt | <file URI>
	logbias         YES      YES   latency | throughput
	mlslabel        YES      YES   <sensitivity label>
	mountpoint      YES      YES   <path> | legacy | none
	nbmand          YES      YES   on | off
	normalization    NO      YES   none | formC | formD | formKC | formKD
	overlay         YES      YES   on | off
	pbkdf2iters      NO       NO   <iters>
	primarycache    YES      YES   all | none | metadata
	quota           YES       NO   <size> | none
	readonly        YES      YES   on | off
	recordsize      YES      YES   512 to 1M, power of 2
	redundant_metadata YES      YES   all | most
	refquota        YES       NO   <size> | none
	refreservation  YES       NO   <size> | none
	relatime        YES      YES   on | off
	reservation     YES       NO   <size> | none
	rootcontext     YES       NO   <selinux rootcontext>
	secondarycache  YES      YES   all | none | metadata
	setuid          YES      YES   on | off
	sharenfs        YES      YES   on | off | share(1M) options
	sharesmb        YES      YES   on | off | sharemgr(1M) options
	snapdev         YES      YES   hidden | visible
	snapdir         YES      YES   hidden | visible
	snapshot_limit  YES       NO   <count> | none
	special_small_blocks YES      YES   zero or 512 to 1M, power of 2
	sync            YES      YES   standard | always | disabled
	utf8only         NO      YES   on | off
	version         YES       NO   1 | 2 | 3 | 4 | 5 | current
	volblocksize     NO      YES   512 to 128k, power of 2
	volmode         YES      YES   default | full | geom | dev | none
	volsize         YES       NO   <size>
	vscan           YES      YES   on | off
	xattr           YES      YES   on | off | dir | sa
	zoned           YES      YES   on | off
	userused@...     NO       NO   <size>
	groupused@...    NO       NO   <size>
	projectused@...  NO       NO   <size>
	userobjused@...  NO       NO   <size>
	groupobjused@...  NO       NO   <size>
	projectobjused@...  NO       NO   <size>
	userquota@...   YES       NO   <size> | none
	groupquota@...  YES       NO   <size> | none
	projectquota@... YES       NO   <size> | none
	userobjquota@... YES       NO   <size> | none
	groupobjquota@... YES       NO   <size> | none
	projectobjquota@... YES       NO   <size> | none
	written@<snap>   NO       NO   <size>

Sizes are specified in bytes with standard units such as K, M, G, etc.

User-defined properties can be specified by using a name containing a colon (:).

The {user|group|project}[obj]{used|quota}@ properties must be appended with
a user|group|project specifier of one of these forms:
    POSIX name      (eg: "matt")
    POSIX id        (eg: "126829")
    SMB name@domain (eg: "matt@sun")
    SMB SID         (eg: "S-1-234-567-89")
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs get compression,compressionratio[C[C[1Pratio[1Pratio[1Pratio
NAME                             PROPERTY       VALUE     SOURCE
poolmirror                       compression    off       default
poolmirror                       compressratio  1.63x     -
poolmirror/data                  compression    off       default
poolmirror/data                  compressratio  1.64x     -
poolmirror/data/doc              compression    off       default
poolmirror/data/doc              compressratio  1.64x     -
poolmirror/data/doc/compressed1  compression    gzip      local
poolmirror/data/doc/compressed1  compressratio  2.69x     -
poolmirror/data/doc/compressed2  compression    gzip-9    local
poolmirror/data/doc/compressed2  compressratio  2.70x     -
poolmirror/data/doc/compressed3  compression    lz4       local
poolmirror/data/doc/compressed3  compressratio  1.64x     -
poolmirror/data/doc/compressed4  compression    lzjb      local
poolmirror/data/doc/compressed4  compressratio  1.37x     -
poolmirror/data/doc/compressed5  compression    zle       local
poolmirror/data/doc/compressed5  compressratio  1.03x     -
poolmirror/mydir                 compression    off       default
poolmirror/mydir                 compressratio  1.00x     -
]0;root@zfs:/home/vagrant[root@zfs vagrant]# zfs get compression,compressratio | grep compressed
poolmirror/data/doc/[01;31m[Kcompressed[m[K1  compression    gzip      local
poolmirror/data/doc/[01;31m[Kcompressed[m[K1  compressratio  2.69x     -
poolmirror/data/doc/[01;31m[Kcompressed[m[K2  compression    gzip-9    local
poolmirror/data/doc/[01;31m[Kcompressed[m[K2  compressratio  2.70x     -
poolmirror/data/doc/[01;31m[Kcompressed[m[K3  compression    lz4       local
poolmirror/data/doc/[01;31m[Kcompressed[m[K3  compressratio  1.64x     -
poolmirror/data/doc/[01;31m[Kcompressed[m[K4  compression    lzjb      local
poolmirror/data/doc/[01;31m[Kcompressed[m[K4  compressratio  1.37x     -
poolmirror/data/doc/[01;31m[Kcompressed[m[K5  compression    zle       local
poolmirror/data/doc/[01;31m[Kcompressed[m[K5  compressratio  1.03x     -
]0;root@zfs:/home/vagrant[root@zfs vagrant]# 
]0;root@zfs:/home/vagrant[root@zfs vagrant]# 
]0;root@zfs:/home/vagrant[root@zfs vagrant]# ll poolmirror/data/doc/compressed1[K{1,2,3,4,5}
ls: cannot access 'poolmirror/data/doc/compressed1': No such file or directory
ls: cannot access 'poolmirror/data/doc/compressed2': No such file or directory
ls: cannot access 'poolmirror/data/doc/compressed3': No such file or directory
ls: cannot access 'poolmirror/data/doc/compressed4': No such file or directory
ls: cannot access 'poolmirror/data/doc/compressed5': No such file or directory
]0;root@zfs:/home/vagrant[root@zfs vagrant]# ll poolmirror/data/doc/compressed{1,2,3,4,5}/poolmirror/data/doc/compressed{1,2,3,4,5}
[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C
/poolmirror/data/doc/compressed1:
total 1230
-rw-r--r--. 1 root root 3291647 Dec  6 10:54 pg2600.txt
-rw-r--r--. 1 root root       0 Dec  6 10:52 War_and_Peace.txt

/poolmirror/data/doc/compressed2:
total 1225
-rw-r--r--. 1 root root 3291647 Dec  6 10:54 pg2600.txt

/poolmirror/data/doc/compressed3:
total 2020
-rw-r--r--. 1 root root 3291647 Dec  6 10:54 pg2600.txt

/poolmirror/data/doc/compressed4:
total 2414
-rw-r--r--. 1 root root 3291647 Dec  6 10:54 pg2600.txt

/poolmirror/data/doc/compressed5:
total 3220
-rw-r--r--. 1 root root 3291647 Dec  6 10:54 pg2600.txt
]0;root@zfs:/home/vagrant[root@zfs vagrant]# ll /poolmirror/data/doc/compressed{1,2,3,4,5}
[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[1P /poolmirror/data/doc/compressed{1,2,3,4,5}
[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[1P /poolmirror/data/doc/compressed{1,2,3,4,5}
[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cd /poolmirror/data/doc/compressed{1,2,3,4,5}
[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cu /poolmirror/data/doc/compressed{1,2,3,4,5}
[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C /poolmirror/data/doc/compressed{1,2,3,4,5}
[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C- /poolmirror/data/doc/compressed{1,2,3,4,5}
[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[Cs /poolmirror/data/doc/compressed{1,2,3,4,5}
[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C[C
1230	/poolmirror/data/doc/compressed1
1225	/poolmirror/data/doc/compressed2
2020	/poolmirror/data/doc/compressed3
2415	/poolmirror/data/doc/compressed4
3221	/poolmirror/data/doc/compressed5
]0;root@zfs:/home/vagrant[root@zfs vagrant]# ll
total 3296
-rw-rw-r--. 1 vagrant vagrant 3291647 Dec  6 10:53 pg2600.txt
-rw-r--r--. 1 root    root      11043 Dec  6 09:55 zfs
-rw-r--r--. 1 root    root      66488 Dec  6 10:56 zfs_homework.md
-rw-r--r--. 1 root    root          0 Dec  6 09:56 zfs.md
]0;root@zfs:/home/vagrant[root@zfs vagrant]# exit

Script done on 2020-12-06 11:09:58+00:00
