    OS:     DEBIAN 12
            lpgitlab1
            10.72.99.252
            4   vcpu
            4GB ram
            dns ajout : lpgitlab1.ad-cimut.priv

    Sites:
        - https://packages.gitlab.com/gitlab/gitlab-ce
        - 
Modif
    nano /etc/hostname
    nano /etc/hosts
    nano /etc/network/interfaces
    sudo reboot

    sudo apt-get install wget perl -y
    cd /tmp/
    wget https://packages.gitlab.com/gitlab/gitlab-ce/packages/debian/bookworm/gitlab-ce_16.7.7-ce.0_amd64.deb

    sudo dpkg -i gitlab-ce_16.7.7-ce.0_amd64.deb
    Modif:
    nano /etc/gitlab/gitlab.rb
    external_url 'lpgitlab1.ad-cimut.priv'

    Reset mdp root : gitlab-rake "gitlab:password:reset"

