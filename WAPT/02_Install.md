    OS:     DEBIAN 12
            plwapt1     10.72.99.250
            plwapt2     10.72.99.249
            plwapt3     10.72.99.248
            4   vcpu
            4GB ram
            dns ajout : plwapt1.ad-cimut.priv
                        plwapt2.ad-cimut.priv
                        plwapt3.ad-cimut.priv

    Sites:
        - https://www.wapt.fr/
        - 
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

Register sur le plwapt1
    sudo wapt-get register
    sudo wapt-get restart-waptservice

    sudo apt install locales-all -y
    sudo localectl set-locale LANG=fr_FR.UTF-8
    sudo localectl status

    sudo timedatectl status

    sudo apt update && apt upgrade -y
    sudo apt install ca-certificates -y

    Suivre la doc : https://www.wapt.fr/fr/doc/
