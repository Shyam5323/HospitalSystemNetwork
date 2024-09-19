# Health Services Network Design

## Project Overview

Melbourne Health Services is a leading health provider in Australia, operating two locations within the same city: the main headquarters and a branch hospital. The goal of this project was to design and implement a robust network infrastructure that meets the requirements set by senior management. The network includes Local Area Network (LAN), Wide Area Network (WAN), and a Server-Side site to enhance network ownership and performance.

### Requirements

- **Network Hierarchical Model**: Implement a hierarchical network model with redundancy using Core routers at HQ and Branch.
- **Network Segmentation**: Each department must have a separate network segment within the same LAN.
- **Subnetting**: Use the base network of 192.168.100.0 for subnetting and allocate IP addresses to each department.
- **Wireless Network**: Provide a wireless network for each department.
- **Security Measures**: Implement Access Control Lists (ACLs) and Virtual Private Network (VPN) to ensure security and performance.
- **Devices and Configuration**: Configure routers, multilayer switches, access switches, DHCP servers, and more.

## Technologies Implemented

- **Network Topology**: Designed using Cisco Packet Tracer.
- **Hierarchical Network Design**: Ensured redundancy and scalability.
- **Basic Device Settings**: Configured hostnames, console passwords, enable passwords, banner messages, and disabled IP domain lookup.
- **VLANs and IP Addressing**: Created VLANs, assigned ports, and configured inter-VLAN routing.
- **DHCP Configuration**: Set up DHCP servers for dynamic IP allocation and static IP for server devices.
- **SSH Configuration**: Enabled SSH for secure remote access.
- **OSPF Routing Protocol**: Configured OSPF for routing and route advertisement.
- **NAT Overload (PAT)**: Configured Port Address Translation for outbound traffic.
- **Site-to-Site IPsec VPN**: Established a secure VPN tunnel between HQ and Branch.
- **Access Control Lists (ACLs)**: Configured both standard and extended ACLs for security.
- **Port Security**: Implemented port security on server-side switches with sticky MAC addresses.
- **Wireless Network**: Configured WLAN using Cisco Access Points.
- **Testing and Verification**: Ensured that all configurations were tested and verified for proper functionality.

## Network Topology

![Network Topology](link-to-your-network-topology-image)

**Headquarters:**
- Departments: Medical Lead Operation & Consultancy Services (MLOCS), Medical Emergency and Reporting (MER), Medical Records Management (MRM), Information Technology (IT), Customer Service (CS)
- Wireless Network: Configured for all departments
- Core Router and Multilayer Switches: Configured for routing and switching

**Branch Hospital:**
- Departments: Nurses & Surgery Operations (NSO), Hospital Labs (HL), Human Resource (HR), Marketing (MK), Finance (FIN)
- Wireless Network: Configured for all departments
- Core Router and Multilayer Switches: Configured for routing and switching

**Server-Side Site:**
- DHCP Server
- DNS Server
- Web Server
- Email Server

## Configuration Details

### Basic Device Configuration
###VLAN and Subnetting
VLAN 10 - MLOCS: 192.168.10.0/24
VLAN 20 - MER: 192.168.20.0/24
VLAN 30 - MRM: 192.168.30.0/24
VLAN 40 - IT: 192.168.40.0/24
VLAN 50 - CS: 192.168.50.0/24
Branch VLANs: Similar subnetting for Branch departments

#### OSPF Configuration
router ospf 1
 network 192.168.0.0 0.0.255.255 area 0

#### VPN Configuration
crypto ikev2 proposal vpn-proposal
 encryption aes-cbc-256
 integrity sha256

crypto ikev2 policy vpn-policy
 proposal vpn-proposal

crypto ipsec transform-set vpn-set esp-aes-256 esp-sha-hmac
 mode tunnel

crypto map vpn-map 10 ipsec-isakmp
 set peer [branch-public-ip]
 set transform-set vpn-set
 match address 101

#### Access Control Lists (ACLs)
access-list 100 permit ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255

#### Port Security
switchport port-security
switchport port-security maximum 1
switchport port-security violation shutdown
switchport port-security mac-address sticky

##Acknowledgements
Cisco Packet Tracer for network simulation and design
Network security and design best practices
