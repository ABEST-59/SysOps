    OS:     DEBIAN 12
            plgitlab2
            10.72.99.252
            4   vcpu
            4GB ram
            dns ajout : plgitlab2.ad-cimut.priv
    Sites:
        - https://packages.gitlab.com/gitlab/gitlab-ce

    Modif:
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

       	sudo apt-get install wget perl -y
       	cd /tmp/
       	wget https://packages.gitlab.com/gitlab/gitlab-ce/packages/debian/bookworm/gitlab-ce_16.7.7-ce.0_amd64.deb
       	sudo dpkg -i gitlab-ce_16.7.7-ce.0_amd64.deb

    Modif:
       	nano /etc/gitlab/gitlab.rb
       	external_url 'lpgitlab1.ad-cimut.priv'
       	Reset mdp root : gitlab-rake "gitlab:password:reset"
