    OS      Debian 12
    IP      10.72.99.253
    CPU     2vCPU
    RAM     2G
    DISK    50G
    LVM     
      PV         VG     Fmt  Attr PSize   PFree
      /dev/sda5  VG_DEB lvm2 a--  <49,52g 21,58g
      VG     #PV #LV #SN Attr   VSize   VFree
      VG_DEB   1   5   0 wz--n- <49,52g 21,58g
      LV   VG     Attr       LSize  Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
      home VG_DEB -wi-ao---- <4,66g
      root VG_DEB -wi-ao----  9,31g
      swap VG_DEB -wi-ao---- <4,66g
      tmp  VG_DEB -wi-ao---- <4,66g
      var  VG_DEB -wi-ao---- <4,66g

    Modif:
        Install:
        sudo apt-get install realmd sssd sssd-tools libnss-sss libpam-sss adcli samba-common-bin packagekit -y
        sudo dpkg -i tis-waptagent-2.5.4.15342-6215c9da-debian-12-amd64.deb && sudo apt --fix-broken install -y 
        sudo wapt-get reset-config-from-url http://plwapt1.ad-cimut.priv/wapt/conf.d/default_f7d90b84633cf6dc45e66833e8cfc29ec2237a207175d18b9ab91dbb25de6f54.json

        Cmd:
        Config SSH
            sed -i.bak -e "s/#Port 22/Port 22/" /etc/ssh/sshd_config
            sed -i.bak -e "s/#PermitRootLogin no/PermitRootLogin no/" /etc/ssh/sshd_config
       Config Resolv
            echo domain ad-cimut.priv >> /etc/resolv.conf
       Config SEC_GVM_TCP timestamps
            echo "#SEC_GVM_Disable TCP timestamp" >> /etc/sysctl.conf
            echo "net.ipv4.tcp_timestamps = 0" >> /etc/sysctl.conf
            sudo sysctl -p
       Config Disable_IPV6
            echo "#Disable IPV6" >> /etc/sysctl.conf
            echo "net.ipv6.conf.all.disable_ipv6 = 1" >> /etc/sysctl.conf
            sudo sysctl -p
