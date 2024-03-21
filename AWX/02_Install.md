
    OS:     DEBIAN 12
            lpawx1
            10.72.99.252
            4   vcpu
            4GB ram
            dns ajout : plawx1.ad-cimut.priv

Modif
    nano /etc/hostname
    nano /etc/hosts
    nano /etc/network/interfaces
    sudo reboot

    sudo realm join ad-cimut.priv --user=adm.sth --computer-ou="OU=prod,OU=Serveurs Linux,OU=Cimut-Ressources,DC=ad-cimut,DC=priv"
    sudo realm deny --all
    sudo realm permit -g gl_infra
    echo "session optional        pam_mkhomedir.so skel=/etc/skel umask=077" >> /etc/pam.d/common-session
    echo "%gl_infra ALL = (ALL) ALL" >> /etc/sudoers.d/ad-cimut
   	sed -i.bak -e "s/use_fully_qualified_names = True/use_fully_qualified_names = False/" /etc/sssd/sssd.conf
	sed -i.bak -e "s/fallback_homedir = \/home\/%u@%d/override_homedir = \/home\/%u/" /etc/sssd/sssd.conf
	echo -e '\n[nss]\nhomedir_substring= /home' >> /etc/sssd/sssd.conf
	systemctl restart sssd 

Register WAPT
    sudo wapt-get register
    sudo wapt-get restart-waptservice

    
    sudo apt-get install curl jq -y
    sudo apt-get install git vim build-essential apparmor apparmor-utils -y

    sudo lvextend -L +10G /dev/VG_DEB/var
    sudo resize2fs /dev/VG_DEB/var
    df -h


Install ANSIBLE
    Install and Use Ansible on Debian 11/10 | ComputingForGeeks
    https://computingforgeeks.com/install-and-use-ansible-on-debian-linux/
    Section : 1b) Install Ansible on Debian 11/10 from Default Upstream Repository.
    sudo apt install ansible
    ansible --version
    ![alt text](image1.png)

Install AWX
    Install Ansible AWX on Debian 12/11/10 |  | ComputingForGeeks 
    https://computingforgeeks.com/how-to-install-ansible-awx-on-debian-buster/
    
