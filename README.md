# Enterprise Layer 3 Switching, DHCP & ACL Security

## Project Overview

This project demonstrates a secure enterprise network designed and implemented using Cisco Packet Tracer.

The network uses a Cisco multilayer switch to perform inter-VLAN routing, centralized DHCP services for automatic IP assignment, and extended Access Control Lists (ACLs) to control communication between departments.

## Project Objectives

- Implement VLAN-based network segmentation.
- Configure inter-VLAN routing using a Layer 3 switch.
- Configure centralized DHCP services.
- Implement DHCP relay using IP helper-address.
- Configure extended ACLs for department-level security.
- Test connectivity and access restrictions.

## Network Devices

- 1 × Cisco 3560 Multilayer Switch
- 3 × Cisco 2960 Access Switches
- 9 × PCs
- 1 × Server-PT

## Network Architecture

| Device | Role |
|---|---|
| MLS1-CORE | Layer 3 core switch |
| SW1-HR | HR access switch |
| SW2-FINANCE | Finance access switch |
| SW3-IT | IT access switch |
| DHCP-SERVER | Central DHCP server |

## VLAN and IP Addressing

| VLAN | Department | Network | Gateway |
|---|---|---|---|
| 10 | HR | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Finance | 192.168.20.0/24 | 192.168.20.1 |
| 30 | IT | 192.168.30.0/24 | 192.168.30.1 |
| 40 | Server | 192.168.40.0/24 | 192.168.40.1 |

## Inter-VLAN Routing

Inter-VLAN routing is implemented using Switch Virtual Interfaces (SVIs) on the Cisco 3560 multilayer switch.

```cisco
ip routing

interface vlan 10
ip address 192.168.10.1 255.255.255.0

interface vlan 20
ip address 192.168.20.1 255.255.255.0

interface vlan 30
ip address 192.168.30.1 255.255.255.0

interface vlan 40
ip address 192.168.40.1 255.255.255.0
```

## DHCP Configuration

A centralized DHCP server provides automatic IP addresses to department PCs.

DHCP pools:
- HR – 192.168.10.0/24
- Finance – 192.168.20.0/24
- IT – 192.168.30.0/24

DHCP relay configuration:

```cisco
interface vlan 10
ip helper-address 192.168.40.10

interface vlan 20
ip helper-address 192.168.40.10

interface vlan 30
ip helper-address 192.168.40.10
```

## ACL Security Configuration

Extended ACLs restrict direct communication between HR and Finance while allowing the configured access to IT and other networks.

### HR ACL

```cisco
ip access-list extended HR-ACL
deny ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255
permit ip 192.168.10.0 0.0.0.255 any

interface vlan 10
ip access-group HR-ACL in
```

### Finance ACL

```cisco
ip access-list extended FINANCE-ACL
deny ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255
permit ip 192.168.20.0 0.0.0.255 any

interface vlan 20
ip access-group FINANCE-ACL in
```

## Verification Commands

```cisco
show vlan brief
show interfaces trunk
show ip interface brief
show ip route
show access-lists
show running-config
```

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS
- Layer 3 Switching
- VLAN
- Inter-VLAN Routing
- DHCP
- DHCP Relay
- Extended ACL
- IPv4 Subnetting

## Learning Outcomes

- Practical enterprise network design.
- Layer 2 and Layer 3 switch configuration.
- Inter-VLAN communication.
- Centralized IP address management.
- Network access control and security.
- Network troubleshooting.

## Author

Andrews GnanaSelvin D

GitHub: https://github.com/Andrewsdavid2005

LinkedIn: https://www.linkedin.com/in/andrews-gnana-selvin-d

## Project Status

Configuration completed. Final connectivity, DHCP and ACL test results should be recorded before claiming full validation.
