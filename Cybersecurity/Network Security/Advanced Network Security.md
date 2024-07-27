# Advanced ACLs and NAT
## Reflexive ACLs
Allows traffic to return only if it was originated from within the network.

**Commands**

    ip access-list extended [name]: Creates an extended access list.
    permit [protocol] [source] [destination] reflect [name]: Configures reflexive ACL entries.
    evaluate [name]: Evaluates reflexive ACL entries.
    
## NAT for IPv6
Stateless NAT64, Stateful NAT64.

**Commands**

    ipv6 nat prefix [prefix]: Configures an IPv6 NAT prefix.
    ipv6 nat v4v6 source [IPv4-address] [IPv6-address]: Configures a source address translation from IPv4 to IPv6.
    ipv6 nat v6v4 source [IPv6-address] [IPv4-address]: Configures a source address translation from IPv6 to IPv4.
    
# Security Protocols and Features
## IPSec VPN Advanced Features
GRE over IPSec, IPSec with IKEv2, DMVPN with IPSec.

**Commands**

    crypto ikev2 proposal [name]: Configures an IKEv2 proposal.
    crypto ikev2 policy [number]: Configures an IKEv2 policy.
    crypto ikev2 keyring [name]: Configures an IKEv2 keyring.
    crypto ikev2 profile [name]: Configures an IKEv2 profile.
    tunnel protection ipsec profile [name]: Applies an IPSec profile to a tunnel interface.
    
## Zone-Based Firewall (ZBF)
Creates security zones, defines policies, and applies them to interfaces.

**Commands**

    zone security [zone-name]: Creates a security zone.
    zone-pair security [name] source [source-zone] destination [destination-zone]: Creates a zone pair.
    class-map type inspect [name]: Defines a class map for inspection.
    policy-map type inspect [name]: Defines a policy map for inspection.
    service-policy type inspect [name]: Applies a policy map to a zone pair.
