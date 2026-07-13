# Device Configuration

This document summarizes the key configurations implemented in this lab. It highlights the commands used to build the network and the purpose of each configuration.


# Switch Configuration

## 1. VLAN Creation

I created separate VLANs to logically divide the network into different departments while using the same physical switch.

![Vlan creation](https://github.com/masib237/IT-HELPDESK-PORTFOLIO/blob/main/VLAN-Segmentation-and-InterVLAN-Routing/Screenshots/creating%20vlans.png?raw=true)



## 2. Assigning Access Ports

Each client PC was connected to an access port and assigned to its respective VLAN.
![access port](https://github.com/masib237/IT-HELPDESK-PORTFOLIO/blob/main/VLAN-Segmentation-and-InterVLAN-Routing/Screenshots/assign%20interfaces%20to%20vlans.png?raw=true)


The same process was repeated for VLAN 30.


## 3. Trunk Configuration

The switch port connected to the router was configured as a trunk.

![trunk config](https://github.com/masib237/IT-HELPDESK-PORTFOLIO/blob/main/VLAN-Segmentation-and-InterVLAN-Routing/Screenshots/make%20router%20port%20trunk.png?raw=true)


### Why a trunk?

The router needed to receive traffic from multiple VLANs over a single physical cable.

A trunk allows frames from different VLANs to travel across the same link by adding VLAN tags

Without a trunk, the link could only carry traffic for a single VLAN.


# Router Configuration

## 1. Router-on-a-Stick

The router was configured with one physical interface and multiple subinterfaces.

Each subinterface represents one VLAN and acts as the default gateway for that network.

Example:
![subinterfaces](https://github.com/masib237/IT-HELPDESK-PORTFOLIO/blob/main/VLAN-Segmentation-and-InterVLAN-Routing/Screenshots/create%20subinterfaces%20and%20turn%20router%20on.png?raw=true)


The physical interface was also enabled using the no shutdown command.


## 2. DHCP Relay

The DHCP server was located in a different VLAN from some client devices.

To allow clients in all VLANs to obtain IP addresses, I configured DHCP relay using the `ip helper-address` command.

Example:
![dhcp relay](https://github.com/masib237/IT-HELPDESK-PORTFOLIO/blob/main/VLAN-Segmentation-and-InterVLAN-Routing/Screenshots/ip%20helper-address%20.png?raw=true)


This forwards DHCP requests from each VLAN to the DHCP server.


# DHCP Server Configuration

The DHCP server was assigned a static IP address.
![dhcp static ip](https://github.com/masib237/IT-HELPDESK-PORTFOLIO/blob/main/VLAN-Segmentation-and-InterVLAN-Routing/Screenshots/assign%20dhcp%20server%20ip.png?raw=true)

Separate DHCP pools were created for each VLAN.
![ip pools](https://github.com/masib237/IT-HELPDESK-PORTFOLIO/blob/main/VLAN-Segmentation-and-InterVLAN-Routing/Screenshots/ip%20address%20pools%20on%20server.png?raw=true)

Each pool included:

- Network address
- Subnet mask
- Default gateway
- Starting IP address

This allowed client devices in each VLAN to automatically receive valid network settings.

# Verification Commands

The following commands were used throughout the lab to verify configurations and troubleshoot issues.

## Switch
show vlan brief-Displays VLANs and assigned switch ports.

show interfaces trunk-Verifies that the trunk link is operational.

## Router

show ip interface brief-Displays interface status and IP addressing.

show running-config-Displays the active router configuration.

show ip route-Displays the router's routing table.


## Client PCs

ipconfig-Verifies assigned IP configuration.
ipconfig /renew-Requests a new DHCP lease.
ping-Tests network connectivity between devices.

![ipconfig&ping](https://github.com/masib237/IT-HELPDESK-PORTFOLIO/blob/main/VLAN-Segmentation-and-InterVLAN-Routing/Screenshots/correct%20ip%20info&ping%20successful.png?raw=true)


# Summary

This configuration demonstrates how VLAN segmentation, trunking, router-on-a-stick, DHCP relay, and dynamic IP addressing work together to provide communication between multiple networks while maintaining logical separation.
