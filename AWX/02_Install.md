
    OS:     DEBIAN 12
            lpawx1
            10.72.99.252
            4   vcpu
            4GB ram
            dns ajout : lpawx1.ad-cimut.priv

Modif
    nano /etc/hostname
    nano /etc/hosts
    nano /etc/network/interfaces
    sudo reboot
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
    
