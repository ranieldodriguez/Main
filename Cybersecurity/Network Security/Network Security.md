# ACLs (Access Control Lists):

## Standard ACLs (1-99):
Filter traffic based on source IP addresses.

### Commands:
    
    access-list [number] [permit|deny] [source]: Creates a standard ACL entry.
    
    ip access-group [number] [in|out]: Applies the ACL to an interface.

## Extended ACLs (100-199):
Filter traffic based on source and destination IP addresses, protocols, and port numbers.

### Commands:
    
    access-list [number] [permit|deny] [protocol] [source] [destination] [port]: Creates an extended ACL entry.
    
    ip access-group [number] [in|out]: Applies the ACL to an interface.

# NAT/PAT (Network Address Translation/Port Address Translation):

## Static NAT:
Maps a single private IP address to a single public IP address.

### Command: 
    ip nat inside source static [local IP] [global IP]
    
## Dynamic NAT:
Maps a private IP address to a public IP address from a pool.

### Commands:
    
    ip nat pool [name] [start-IP] [end-IP] netmask [mask]: Defines a pool of public IP addresses.
    
    ip nat inside source list [number] pool [name]: Configures NAT using the defined pool.

## PAT (Overloading):
Maps multiple private IP addresses to a single public IP address using different ports.

### Command: 

    ip nat inside source list [number] interface [type] overload

# Security Protocols:

## SSH (Secure Shell):
Provides a secure channel over an unsecured network.

## AAA (Authentication, Authorization, and Accounting):
Framework for configuring a set of three independent security functions.

## TACACS+ (Terminal Access Controller Access-Control System Plus):
Cisco protocol for AAA.

## RADIUS (Remote Authentication Dial-In User Service):
Protocol for AAA, used for network access.
