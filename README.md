# ZFS_01_stand
**Установка ZFS**
1. Поднимаем виртуалку
2. Добавляем 3 SATA диска
3. Устанавливаем ZFS

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
