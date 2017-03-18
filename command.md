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
mkdir /mnt/boot
pacstrap /mnt base base-devel
genfstab -p /mnt >> /mnt/etc/fstab
arch-chroot /mnt
echo ccr > /etc/hostname
vi /etc/timezone -> Asia/Seoul
vi /etc/locale.gen -> en_US.UTF-8 UTF-8, ko_KR.UTF-8 UTF-8
locale-gen
hwclock --systohc --utc
pacman -S grub-bios
grub-install --target=i386-pc --recheck /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
mkinitcpio -p linux
passwd
useradd -m -g users -G storage,power,wheel -s /bin/bash ccr
passwd ccr
pacman -S sudo gksu
vi /etc/sudoers -> ALL=(ALL) ALL
%wheel ALL=(ALL) ALL
exit
umount -R /mnt
reboot
pacman -S dialog wpa_supplicant networkmanager
pacman -S xf86-video-intel xorg-server gdm gnome gnome-shell
pacman -S xterm
systemctl enable gdm.service
systemctl enable NetworkManager

'/etc/pacman.conf'

[archlinuxfr]
SigLeven = Never
Server = http://repo.archlinux.fr/$arch

#pacman -Sy yaourt

#pacman -S ibus ibus-hangul

'~/.bashrc'
export GTK_IM_MODULE="ibus"
export XMODIFIERS="@im=ibus"
export QT_IM_MODULE="ibus"

$ibus-setup
$ibus-setup-hangul

#yaourt -S ttf-nanum ttf-nanumgothic_coding

'System Setting -> Region&Language -> Add English and Korean'

yaourt -S wget

yaourt -S sublime-text-dev
ln -s /opt/sublime_text_3/sublime_text /usr/bin/sublime


