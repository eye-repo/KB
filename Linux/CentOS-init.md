Set hostname
    
    hostnamectl set-hostname vcentos

Update host
    
    yum update
    yum upgrade

Set timezone
    
    mv /etc/localtime /etc/localtime.init
    ln -s  /usr/share/zoneinfo/Europe/Warsaw /etc/localtime

Remove GUI mode booting screen
    
    cp /etc/default/grub /etc/default/grub.$(date +%Y%m%d%H%M%S).bak
    sed -i 's/ rhgb//g' /etc/default/grub
    grub2-mkconfig -o /etc/grub2.cfg

Install VirtualBox Guest Additions
    
    yum install tar bzip2 gcc make perl
    yum install kernel-headers kernel-devel elfutils-libelf-devel
    mount /dev/cdrom  /mnt/
    /mnt/VBoxLinuxAdditions.run

Install additional packages
    
    yum install vim wget bash-completion bind-utils

Install optional software
    
    yum install epel-release
    yum update
    yum install pwgen sshpass

Other software
    
    yum install cifs-utils
