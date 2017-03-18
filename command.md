ip addr
ip link
systemctl start dhcpcd@enp4s0
umount /dev/sda
cfdisk /dev/sda -> 8333:linux 82:swap
fdisk -l
mkfs.ext4 /dev/sda1
mkswap /dev/sda2
swapon /dev/sda2
mount /dev/sda1 /mnt

