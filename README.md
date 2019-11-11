## Ubuntu


### 1. Network

**Setting hostname**
 - `hostname` (to show hostname)
 - `cat /etc/hostname` 
   - the hostnamectl command doesn't update `/etc/hosts` for you, so you'll need to edit that file yourself.
    
**Managing network interface**
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