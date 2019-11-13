## Ubuntu


### 1. Network

**Setting hostname**
 - `hostname` (to show hostname)
 - `cat /etc/hostname` 
   - the hostnamectl command doesn't update `/etc/hosts` for you, so you'll need to edit that file yourself.
    
**Managing network interface**
- use ***Netplan***
- `ip addr show`;
- can bring a device down, and then back up again:
  - `sudo ip link set enp0s3 down`
  - `sudo ip link set enp0s3 up`

**Assigning static IP addresses**
- check */etc/netplan* (ls `/etc/netplan`)
- change to:
```
# This file describes the network interfaces available on your system 
# For more information, see netplan(5). 
network:
  version: 2
  renderer: networkd
    ethernets:
     enp0s3:
      dhcp4: no
      addresses: [192.168.1.132/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [192.168.1.1,8.8.8.8] 
```
- To actually make these changes take effect you can run the following command: `sudo netplan apply`

**NetworkManager**
- `sudo systemctl stop NetworkManager`
- `sudo systemctl disable NetworkManager`
- `sudo systemctl restart networking`

**OpenSSH**
- type `which sshd`, if you have OpenSSH Server installed, your output should read */usr/sbin/sshd*
- `sudo apt install openssh-server`
- type `which ssh`, if you have OpenSSH Client installed, your output should read */usr/sbin/sshd*
- `sudo apt install openssh-client `
- verify is *openssh-server* is running `systemctl status ssh`
- if *openssh-server* is not running `sudo systemctl start ssh`
- if *openssh-server* doesn't start up automatically when the server boots `sudo systemctl enable ssh`
- if *netstat* not installed `sudo apt-get install net-tools`
- list listening ports `sudo netstat -tulpn |grep ssh`
- to connect to a server using SSH `ssh 192.168.1.132`
- to connect to a server using SSH with different username `ssh username@10.10.96.10`
- to connect to a server using SSH with different username and different port `ssh -p 2021 username@10.10.96.10`
- TODO: add ssh key manager

**Hardware updates**
- Ubuntu features a set of updates known as the hardware enablement (HWE) stack
  - DESKTOP `sudo apt-get install --install-recommends linux-generic-hwe-18.04 xserver-xorg-hwe-18.04`
  - SERVER `sudo apt-get install --install-recommends linux-generic-hwe-18`
  
**Installing and removing software**
- APT (Advanced Package Tool) 
  - `sudo apt install <package>`
  - `sudo apt update <package>`
  - `sudo apt remove <package>`
  - `apt search <search term>`
    - old version apt-get
- SNAP 
  - `sudo snap install <package>`
  - `sudo snap refresh <package>`
  - `sudo snap remove <package>`
  - `snap find <search term>`
  
**Showing running processes**
- `ps`, `ps a`, `ps au`, `ps aux`, `ps aux | grep nginx`, `ps u -C nginx `, `ps aux --sort=-pcpu`, `ps aux --sort=-pcpu | head -n 5`, `ps aux --sort=-pmem | head -n 5`