# NAT (Network Address Translation) Commands:

**Static NAT**: Maps a single private IP address to a single public IP address.

*Command*: ip nat inside source static [local IP] [global IP]

    Example: ip nat inside source static 192.168.1.10 203.0.113.10

**Dynamic NAT**: Maps a private IP address to a public IP address from a pool.

*Commands*: ip nat pool [name] [start-IP] [end-IP] netmask [mask]

    Example: ip nat pool mypool 203.0.113.1 203.0.113.254 netmask 255.255.255.0
    ip nat inside source list [number] pool [name]
    Example: ip nat inside source list 1 pool mypool
    
**PAT (Overloading)**: Maps multiple private IP addresses to a single public IP address using different ports.

*Command*: ip nat inside source list [number] interface [type] overload

    Example: ip nat inside source list 1 interface GigabitEthernet0/0 overload

# VPN (Virtual Private Network) Technologies:

**GRE (Generic Routing Encapsulation)**: Encapsulates a wide variety of network layer protocols inside point-to-point connections.

*Command*:

interface Tunnel0

ip address [address] [mask]

tunnel source [source-interface]


tunnel destination [destination-ip]

**IPSec (Internet Protocol Security)**: Provides secure communication over IP networks through authentication and encryption.

*Commands*:

crypto isakmp policy [number]  
- Specifies the ISAKMP policy.

crypto ipsec transform-set [name] [transform1] [transform2]
- Specifies the transform set for IPSec.

crypto map [name] [sequence-number] ipsec-isakmp
- Creates a crypto map for IPSec.

**DMVPN (Dynamic Multipoint Virtual Private Network)**: Allows for the creation of dynamic, scalable VPNs.

*Commands*:

interface Tunnel0
- Configures a DMVPN tunnel interface.

ip nhrp network-id [id]
- Specifies the NHRP network ID.

tunnel source [source-interface]
- Specifies the source interface for the tunnel.

tunnel mode gre multipoint
- Specifies the tunnel mode as GRE multipoint.
