# DHCP (Dynamic Host Configuration Protocol):

## Commands:
    
    ip dhcp pool [name]: Creates a DHCP pool.
    
    network [network]: Specifies the network for the DHCP pool.
    
    default-router [address]: Specifies the default gateway for the DHCP clients.
    
    dns-server [address]: Specifies the DNS server for the DHCP clients.
    
    lease [days]: Specifies the lease duration for DHCP clients.
    
    ip helper-address [address]: Forwards DHCP requests to a remote DHCP server.

# DNS (Domain Name System):

## Commands:
    
    ip name-server [address]: Specifies the DNS server IP address.
    
    ip domain-lookup: Enables DNS-based hostname-to-IP address translation.

# NTP (Network Time Protocol):

## Commands:

    ntp server [address]: Specifies the NTP server IP address.
    
    ntp update-calendar: Synchronizes the system calendar.
    
    clock set [time] [date]: Manually sets the system clock.

# SNMP (Simple Network Management Protocol):

## Commands:
    
    snmp-server community [community-string] [RO|RW]: Configures the community string for SNMP.
    
    snmp-server location [location]: Sets the physical location of the device.
    
    snmp-server contact [contact]: Sets the contact information for the device.

# Advanced DHCP and DNS
## DHCP Options and IPv6 DHCP

**Commands**

    ip dhcp pool [name]: Creates a DHCP pool.
    option [option-code] [value]: Configures DHCP options.
    ipv6 dhcp pool [name]: Creates a DHCPv6 pool.
    address prefix [prefix]: Configures an IPv6 prefix in a DHCPv6 pool.
    dns-server [address]: Configures a DNS server in a DHCP pool.
    domain-name [name]: Configures a domain name in a DHCP pool.   

# Advanced NTP and SNMP
## NTP Authentication and Access Control

**Commands**

    ntp authenticate: Enables NTP authentication.
    ntp authentication-key [key-id] md5 [key]: Configures an NTP authentication key.
    ntp trusted-key [key-id]: Specifies trusted NTP keys.
    ntp access-group [access-group]: Configures NTP access control.

## SNMPv3: Enhanced security with authentication and encryption

**Commands**
    
    snmp-server group [name] v3 [auth|priv]: Creates an SNMPv3 group.
    snmp-server user [username] [group] v3 [auth|priv] [password]: Creates an SNMPv3 user.
    snmp-server host [host-address] version 3 [auth|priv] [username]: Configures an SNMPv3 host.
