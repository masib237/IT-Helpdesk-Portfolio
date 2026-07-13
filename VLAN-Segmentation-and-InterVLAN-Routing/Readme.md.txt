# VLAN Segmentation and Inter-VLAN Routing Lab (Router-on-a-Stick)

## Overview

I created this network to simulate a small office environment where different departments are separated into their own logical networks using VLANs.

The goal of this lab was to understand how VLAN segmentation works, how devices in different VLANs communicate, and how services such as DHCP operate when multiple networks are involved.

Before implementing VLANs, all devices would exist in one flat network where they shared the same broadcast domain. In a real organization, this approach is not ideal because it affects security, performance, and network management.

To solve this, I separated devices into different VLANs and implemented inter-VLAN routing using a router-on-a-stick configuration.



# Objectives

The main objectives of this lab were:

- Create and configure VLANs on a switch
- Assign switch ports to specific VLANs
- Configure a trunk link between a switch and router
- Configure router subinterfaces for inter-VLAN routing
- Configure a DHCP server to provide IP addresses dynamically
- Configure DHCP relay using ip helper-address
- Test communication between different VLANs
- Troubleshoot common networking issues



# Network Design

The network consists of:

- 1 Router
- 1 Layer 2 Switch
- 1 DHCP Server
- Multiple client PCs

The switch was configured with multiple VLANs representing different departments:

- VLAN 10 for the HR Department
- VLAN 20 for the IT Department
- VLAN 30 for the Finance Department

Each VLAN represents a separate broadcast domain.



# Why VLANs Were Implemented

I created separate VLANs to simulate how organizations separate users and devices based on departments or security requirements.

For example:

- Finance users can exist in one VLAN
- IT users can exist in another VLAN and Finance users in another VLAN
- Guest devices can exist in another VLAN(to be added)

Although all devices connect to the same physical switch, VLANs allow them to operate as separate logical networks.


# Inter-VLAN Routing

After creating VLANs, devices in different VLANs could no longer communicate directly because each VLAN became its own network.

To allow communication between VLANs, I configured router-on-a-stick.

This involved:

1. Configuring the switch port(Gig0/1) connected to the router as a trunk port.

2. Creating router subinterfaces for each VLAN.

3. Assigning each subinterface a default gateway IP address.

Example:

VLAN 10 Gateway:
192.168.10.1

VLAN 20 Gateway:
192.168.20.1

VLAN 30 Gateway:
192.168.30.1

The router acts as the Layer 3 device responsible for routing traffic between VLANs.


# Why the Trunk Link Was Required

The router and switch were connected using one physical cable.

Since multiple VLANs needed to communicate with the router, the connection had to carry traffic from VLAN 10, VLAN 20, and VLAN 30 simultaneously.

I configured the switch port as a trunk, allowing multiple VLANs to pass through the same physical link using VLAN tagging.


# DHCP Configuration

The DHCP server was configured with separate address pools for each VLAN.

Each pool provided:

- IP addresses
- Default gateway
- DNS information

Because DHCP broadcasts do not cross routers automatically, I configured DHCP relay using:

ip helper-address

on each router subinterface.

This allowed clients in different VLANs to obtain IP addresses from the centralized DHCP server.



# Testing and Verification

After completing the configuration, I verified:

- VLAN assignments on the switch
- Trunk status between switch and router
- Router subinterfaces
- DHCP address assignment
- Connectivity between devices in different VLANs

Testing included:

- Checking assigned IP addresses
- Using ping between devices
- Verifying communication between VLANs



# Skills Practiced

Through this lab, I practiced:

- VLAN configuration
- Switch port configuration
- 802.1Q trunking
- Router-on-a-stick
- DHCP configuration
- DHCP relay
- IP addressing
- Network troubleshooting
- Basic enterprise network design


# Lessons Learned

This lab helped me understand that creating VLANs is not only about separating devices.

Once a network is divided into VLANs, additional configuration is required for communication and services to work correctly.

A major lesson was understanding that DHCP broadcasts do not automatically cross VLAN boundaries, which is why DHCP relay is required in routed environments.