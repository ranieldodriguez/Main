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
