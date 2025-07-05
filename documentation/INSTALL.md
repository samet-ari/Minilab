# Installation Guide - MiniLab Project

## 🖥️ VM Requirements

### NFS Server (Gateway)
- **CPU**: 2 cores
- **RAM**: 1GB  
- **Storage**: 8GB system + 4x8GB disks (RAID 5)
- **Network**: 2 interfaces (WAN + LAN)
- **IP**: 192.168.15.254
- **Services**: NFS, OpenVPN, Firewall, Gateway

### DHCP Servers (x2)
- **CPU**: 1 core each
- **RAM**: 1GB each
- **Storage**: 8GB each
- **Network**: LAN interface
- **IPs**: 192.168.15.253 (DHCP1), 192.168.15.252 (DHCP2)
- **Services**: DHCP, DNS, LDAP, Keepalived

### Client VMs
- **CPU**: 1 core
- **RAM**: 1GB
- **Storage**: 16GB
- **Network**: LAN interface
- **IPs**: DHCP range 192.168.15.100-150

## 🔧 Installation Order

### Phase 1: Network Infrastructure
1. **VM Setup**: Create and configure all VMs
2. **Network**: Configure 192.168.15.0/24 internal network
3. **Static IPs**: Configure server static IPs
4. **SSH Access**: Enable SSH on all servers

### Phase 2: Core Services
1. **DHCP Master/Slave**: Install ISC DHCP Server
2. **DNS Master/Slave**: Install and configure Bind9
3. **LDAP**: Install OpenLDAP for authentication
4. **Keepalived**: Configure virtual IP failover

### Phase 3: Storage & Authentication
1. **RAID 5**: Configure storage on NFS Server
2. **NFS Server**: Export /export/home directory
3. **PAM-LDAP**: Configure client authentication
4. **User Creation**: Create LDAP users

### Phase 4: Security
1. **Firewall**: Configure iptables rules
2. **OpenVPN**: Setup VPN server with certificates
3. **MFA**: Implement Google Authenticator
4. **Access Control**: Secure all services

### Phase 5: Testing & Validation
1. **DHCP Tests**: Verify load balancing
2. **DNS Tests**: Test forward/reverse resolution
3. **Authentication**: Test LDAP user login
4. **Failover**: Test high availability
5. **End-to-End**: Complete integration tests

## 🌐 Network Configuration
192.168.15.0/24 (Internal Network)
├── 192.168.15.1 (Gateway)
├── 192.168.15.250 (Virtual IP - Failover)
├── 192.168.15.252 (DHCP2 - Slave)
├── 192.168.15.253 (DHCP1 - Master)
├── 192.168.15.254 (NFS Server)
└── 192.168.15.100-150 (DHCP Pool)
10.8.0.0/24 (VPN Network)
├── 10.8.0.1 (VPN Server)
└── 10.8.0.4+ (VPN Clients)
## 📚 Key Configuration Files

- `/etc/dhcp/dhcpd.conf` - DHCP server configuration
- `/etc/keepalived/keepalived.conf` - HA configuration
- `/etc/bind/named.conf.local` - DNS zones
- `/etc/exports` - NFS exports
- `/etc/openvpn/server.conf` - VPN configuration
- `/etc/iptables/rules.v4` - Firewall rules

## ✅ Validation Commands

```bash
# DHCP Status
systemctl status isc-dhcp-server

# DNS Resolution
nslookup dhcp1.linuxisgood.local

# LDAP Authentication  
getent passwd testuser

# NFS Mount
showmount -e 192.168.15.254

# Failover IP
ip addr show | grep 192.168.15.250