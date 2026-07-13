# Troubleshooting Notes

## Issue: PC4 Received 169.254.x.x Addresses
![apipa](https://github.com/masib237/IT-HELPDESK-PORTFOLIO/blob/main/VLAN-Segmentation-and-InterVLAN-Routing/Screenshots/APIPA%20ip%20issue.png?raw=true)

### Symptoms

After configuring VLANs, some PCs failed to receive IP addresses and automatically assigned themselves APIPA addresses,i.e,169.254.168.56


### Cause

The DHCP server was located in a different VLAN from the client devices.

DHCP uses broadcast messages when requesting an IP address. These broadcasts cannot cross routers without additional configuration.


### Solution

I configured DHCP relay on the router using:

ip helper-address

on each VLAN subinterface.

I also created separate DHCP pools for each VLAN.
![apipa](https://github.com/masib237/IT-HELPDESK-PORTFOLIO/blob/main/VLAN-Segmentation-and-InterVLAN-Routing/Screenshots/APIPA%20ip%20issue.png?raw=true)


### Verification

After applying the changes:

- PCs successfully received valid IP addresses
- Default gateways were assigned correctly
- Devices in different VLANs were able to communicate
  ![apipa](https://github.com/masib237/IT-HELPDESK-PORTFOLIO/blob/main/VLAN-Segmentation-and-InterVLAN-Routing/Screenshots/APIPA%20ip%20issue.png?raw=true)
