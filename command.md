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

pacman -S openssh

'/etc/ssh/ssh_config'
ListenAddress 0.0.0.0
ChallengeResponseAuthentication no
UsePAM yes
Subsystem sftp /usr/lib/ssh/sftp-server

'/etc/hosts.allow'
sshd: ALL

'/etc/hots.deny'

systemctl start sshd
systemctl enable sshd

sudo shown -R USERNAME /home/USERNAME

pacman -S git
git config --global user.name "..."
git config --global user.email "...."

pacman -S ninja

pacman -S dante

'/etc/sockd.conf'
logoutput: /var/log/sockd.log
logoutput: stderr
debug: 9

internal: enp3s0 port = 1080
internal: 127.0.0.1 port = 1080

external: enp3s0

compatibility: sameport

extension: bind

external.rotation: route

user.privileged: root

user.notprivileged: ccr

clientmethod: none

socksmethod: pam.username

# Who can access this proxy?
# Accept only connections from the loopback, all ports
client pass {
 from: 0.0.0.0/0 to: 0.0.0.0/0
}

#Block all other connection attempts
client block {
 from: 0.0.0.0/0 to: 0.0.0.0/0
 log: connect error
}

# Once connected, where can they go?
socks block {
 from: 0.0.0.0/0 to: 127.0.0.0/8
 log: connect error
}

#Pass from the internal IP to anywhere
socks pass {
 from: 192.168.0.0/16 to: 0.0.0.0/0
 protocol: tcp udp
}

#Pass from the loopback going anywhere
socks pass {
 from: 0.0.0.0/0 to: 0.0.0.0/0
 protocol: tcp udp
}

# Block everything else
socks block {
 from: 0.0.0.0/0 to: 0.0.0.0/0
 log: connect error
}

systemctl enable sockd
systemctl start sockd
systmctl status -l sockd

pacman -S chromium

pacman -S vlc
pacman -S qt4

tar xvjf file.bz2


