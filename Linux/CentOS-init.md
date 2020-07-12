# Init commands after Centos\RedHat install

- Set hostname

      hostnamectl set-hostname vcentos

- Update host

      yum update
      yum upgrade

- Set timezone

      mv /etc/localtime /etc/localtime.init
      ln -s  /usr/share/zoneinfo/Europe/Warsaw /etc/localtime

- Remove GUI mode booting screen

      cp /etc/default/grub /etc/default/grub.$(date +%Y%m%d%H%M%S).bak
      sed -i 's/ rhgb//g' /etc/default/grub
      grub2-mkconfig -o /etc/grub2.cfg

- Install VirtualBox Guest Additions

      yum install tar bzip2 gcc make perl
      yum install kernel-headers kernel-devel elfutils-libelf-devel
      mount /dev/cdrom  /mnt/
      /mnt/VBoxLinuxAdditions.run

- Install additional packages

      yum install vim wget bash-completion bind-utils

- Install optional software

      yum install epel-release
      yum update
      yum install pwgen sshpass

- Other software

      yum install cifs-utils

- Mount DVD Repo

    Mount iso or cd-rom\dvd-rom

      mkdir -p  /mnt/disc
      mount -o loop RHEL7.1.iso /mnt/disc
      # or
      mkdir -p  /mnt/disc
      mount /dev/sr0  /mnt/disc

    Copy repo file

      cp /mnt/disc/media.repo /etc/yum.repos.d/dvd.repo
      chmod 644 /etc/yum.repos.d/dvd.repo

    Edit repo file

      echo "enabled=1" >> /etc/yum.repos.d/dvd.repo
      echo "baseurl=file:///mnt/disc/" >> /etc/yum.repos.d/dvd.repo
      echo "gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release" >> /etc/yum.repos.d/dvd.repo

      # or use editor:
      vim /etc/yum.repos.d/dvd.repo

      enabled=1
      baseurl=file:///mnt/disc/
      gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

    Check repofile:

      cat /etc/yum.repos.d/dvd.repo
      [DVD Repo]
      name=DVD Repo
      mediaid=123456780.654321
      metadata_expire=-1
      gpgcheck=1
      cost=500
      enabled=1
      baseurl=file:///mnt/disc/
      gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

    Check repo with `yum`

      yum clean all
      yum repolist enabled
      yum update
