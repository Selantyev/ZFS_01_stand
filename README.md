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
