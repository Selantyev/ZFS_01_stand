# ZFS_01_stand
**Установка ZFS**
1. Поднимаем виртуалку
2. Добавляем 4 SATA диска
3. Устанавливаем ZFS (CentOS8)

`yum install -y yum-utils`

`yum install -y http://download.zfsonlinux.org/epel/zfs-release.el8_2.noarch.rpm`

`gpg --quiet --with-fingerprint /etc/pki/rpm-gpg/RPM-GPG-KEY-zfsonlinux`

`yum-config-manager --enable zfs-kmod`

`yum-config-manager --disable zfs`

`yum install -y zfs`

`modprobe zfs`

**Определить алгоритм с наилучшим сжатием**
1. Созданы файловые системы с разными типами сжатия

```
# zfs get compression
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
```
2. Скачан файл http://www.gutenberg.org/ebooks/2600.txt.utf-8
3. Файл скопирован в каждую файловую систему

```
# cp pg2600.txt /poolmirror/data/doc/compressed1
# cp pg2600.txt /poolmirror/data/doc/compressed2
# cp pg2600.txt /poolmirror/data/doc/compressed3
# cp pg2600.txt /poolmirror/data/doc/compressed4
# cp pg2600.txt /poolmirror/data/doc/compressed5
```
4. Определим лучший тип сжатия

```
# zfs get compression,compressratio | grep compressed
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
```

```
# du -s /poolmirror/data/doc/compressed{1,2,3,4,5}
1230    /poolmirror/data/doc/compressed1
1225    /poolmirror/data/doc/compressed2
2020    /poolmirror/data/doc/compressed3
2415    /poolmirror/data/doc/compressed4
3221    /poolmirror/data/doc/compressed5
```

5. Лучший тип сжатия

```
poolmirror/data/doc/compressed2  compression    gzip-9    local
poolmirror/data/doc/compressed2  compressratio  2.70x     -
```

**Определить настройки пула**
1. Скачать файл

`wget --no-check-certificate -O zfs_task1.tar.gz 'https://drive.google.com/open?id=1KRBNW33QWqbvbVHa3hLJivOAt60yukkg'`

2. Распаковать 

`tar -xvf zfs_task1.tar.gz`

3. Отключаем текущие диски
`zpool export storage`
`zpool status`

4. Импортируем zfs из файла

`zpool import -d ./zpoolexport/ otus`

5. Проверяем статус

`zpool status`

```
  pool: otus
 state: ONLINE
  scan: none requested
config:

        NAME                                 STATE     READ WRITE CKSUM
        otus                                 ONLINE       0     0     0
          mirror-0                           ONLINE       0     0     0
            /home/vagrant/zpoolexport/filea  ONLINE       0     0     0
            /home/vagrant/zpoolexport/fileb  ONLINE       0     0     0

errors: No known data errors
```

`zfs list`

```
NAME             USED  AVAIL     REFER  MOUNTPOINT
otus            2.04M   350M       24K  /otus
otus/hometask2  1.88M   350M     1.88M  /otus/hometask2
```

`# zpool list`

```
NAME   SIZE  ALLOC   FREE  CKPOINT  EXPANDSZ   FRAG    CAP  DEDUP    HEALTH  ALTROOT
otus   480M  2.09M   478M        -         -     0%     0%  1.00x    ONLINE  -
```

`# zfs get all`

```
NAME            PROPERTY              VALUE                  SOURCE
otus            type                  filesystem             -
otus            creation              Fri May 15  4:00 2020  -
otus            used                  2.04M                  -
otus            available             350M                   -
otus            referenced            24K                    -
otus            compressratio         1.00x                  -
otus            mounted               yes                    -
otus            quota                 none                   default
otus            reservation           none                   default
otus            recordsize            128K                   local
otus            mountpoint            /otus                  default
otus            sharenfs              off                    default
otus            checksum              sha256                 local
otus            compression           zle                    local
otus            atime                 on                     default
otus            devices               on                     default
otus            exec                  on                     default
otus            setuid                on                     default
otus            readonly              off                    default
otus            zoned                 off                    default
otus            snapdir               hidden                 default
otus            aclinherit            restricted             default
otus            createtxg             1                      -
otus            canmount              on                     default
otus            xattr                 on                     default
otus            copies                1                      default
otus            version               5                      -
otus            utf8only              off                    -
otus            normalization         none                   -
otus            casesensitivity       sensitive              -
otus            vscan                 off                    default
otus            nbmand                off                    default
otus            sharesmb              off                    default
otus            refquota              none                   default
otus            refreservation        none                   default
otus            guid                  14592242904030363272   -
otus            primarycache          all                    default
otus            secondarycache        all                    default
otus            usedbysnapshots       0B                     -
otus            usedbydataset         24K                    -
otus            usedbychildren        2.01M                  -
otus            usedbyrefreservation  0B                     -
otus            logbias               latency                default
otus            objsetid              54                     -
otus            dedup                 off                    default
otus            mlslabel              none                   default
otus            sync                  standard               default
otus            dnodesize             legacy                 default
otus            refcompressratio      1.00x                  -
otus            written               24K                    -
otus            logicalused           1020K                  -
otus            logicalreferenced     12K                    -
otus            volmode               default                default
otus            filesystem_limit      none                   default
otus            snapshot_limit        none                   default
otus            filesystem_count      none                   default
otus            snapshot_count        none                   default
otus            snapdev               hidden                 default
otus            acltype               off                    default
otus            context               none                   default
otus            fscontext             none                   default
otus            defcontext            none                   default
otus            rootcontext           none                   default
otus            relatime              off                    default
otus            redundant_metadata    all                    default
otus            overlay               off                    default
otus            encryption            off                    default
otus            keylocation           none                   default
otus            keyformat             none                   default
otus            pbkdf2iters           0                      default
otus            special_small_blocks  0                      default
otus/hometask2  type                  filesystem             -
otus/hometask2  creation              Fri May 15  4:18 2020  -
otus/hometask2  used                  1.88M                  -
otus/hometask2  available             350M                   -
otus/hometask2  referenced            1.88M                  -
otus/hometask2  compressratio         1.00x                  -
otus/hometask2  mounted               yes                    -
otus/hometask2  quota                 none                   default
otus/hometask2  reservation           none                   default
otus/hometask2  recordsize            128K                   inherited from otus
otus/hometask2  mountpoint            /otus/hometask2        default
otus/hometask2  sharenfs              off                    default
otus/hometask2  checksum              sha256                 inherited from otus
otus/hometask2  compression           zle                    inherited from otus
otus/hometask2  atime                 on                     default
otus/hometask2  devices               on                     default
otus/hometask2  exec                  on                     default
otus/hometask2  setuid                on                     default
otus/hometask2  readonly              off                    default
otus/hometask2  zoned                 off                    default
otus/hometask2  snapdir               hidden                 default
otus/hometask2  aclinherit            restricted             default
otus/hometask2  createtxg             216                    -
otus/hometask2  canmount              on                     default
otus/hometask2  xattr                 on                     default
otus/hometask2  copies                1                      default
otus/hometask2  version               5                      -
otus/hometask2  utf8only              off                    -
otus/hometask2  normalization         none                   -
otus/hometask2  casesensitivity       sensitive              -
otus/hometask2  vscan                 off                    default
otus/hometask2  nbmand                off                    default
otus/hometask2  sharesmb              off                    default
otus/hometask2  refquota              none                   default
otus/hometask2  refreservation        none                   default
otus/hometask2  guid                  3809416093691379248    -
otus/hometask2  primarycache          all                    default
otus/hometask2  secondarycache        all                    default
otus/hometask2  usedbysnapshots       0B                     -
otus/hometask2  usedbydataset         1.88M                  -
otus/hometask2  usedbychildren        0B                     -
otus/hometask2  usedbyrefreservation  0B                     -
otus/hometask2  logbias               latency                default
otus/hometask2  objsetid              81                     -
otus/hometask2  dedup                 off                    default
otus/hometask2  mlslabel              none                   default
otus/hometask2  sync                  standard               default
otus/hometask2  dnodesize             legacy                 default
otus/hometask2  refcompressratio      1.00x                  -
otus/hometask2  written               1.88M                  -
otus/hometask2  logicalused           963K                   -
otus/hometask2  logicalreferenced     963K                   -
otus/hometask2  volmode               default                default
otus/hometask2  filesystem_limit      none                   default
otus/hometask2  snapshot_limit        none                   default
otus/hometask2  filesystem_count      none                   default
otus/hometask2  snapshot_count        none                   default
otus/hometask2  snapdev               hidden                 default
otus/hometask2  acltype               off                    default
otus/hometask2  context               none                   default
otus/hometask2  fscontext             none                   default
otus/hometask2  defcontext            none                   default
otus/hometask2  rootcontext           none                   default
otus/hometask2  relatime              off                    default
otus/hometask2  redundant_metadata    all                    default
otus/hometask2  overlay               off                    default
otus/hometask2  encryption            off                    default
otus/hometask2  keylocation           none                   default
otus/hometask2  keyformat             none                   default
otus/hometask2  pbkdf2iters           0                      default
otus/hometask2  special_small_blocks  0                      default
```

**Найти сообщение от преподавателей**
1. Скачать файл 
https://drive.google.com/file/d/1gH8gCL9y7Nd5Ti3IRmplZPF1XjzxeRAG/view?usp=sharing созданый командой:

`zfs send otus/storage@task2 > otus_task2.filе`
или
`zfs snapshot storage/data/music@snap001`

2. Восстанавливаем снэпшот из файла

`zfs receive -F otus/hometask2 < ./otus_task2.file`

3. Найти сообщение

```
cat /otus/hometask2/task1/file_mess/secret_message
https://github.com/sindresorhus/awesome
```
