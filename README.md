## Ubuntu


#### 1. Network

**Setting hostname**
 - `hostname` (to show hostname)
 - `cat /etc/hostname` 
   - the hostnamectl command doesn't update `/etc/hosts` for you, so you'll need to edit that file yourself.
    
**Managing network interface**
- `ip addr show`;
- can bring a device down, and then back up again:
  - `sudo ip link set enp0s3 down`
  - `sudo ip link set enp0s3 up`
