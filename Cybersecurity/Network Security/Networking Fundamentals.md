## 1. Networking Fundamentals

### OSI Model Layers:

Physical

Data Link

Network

Transport

Session

Presentation

Application

### TCP/IP Model Layers:

Network Interface

Internet

Transport

Application

### Common Protocols:

HTTP/HTTPS, FTP, SSH, Telnet, DNS, DHCP, ARP, ICMP

### IP Addressing:

#### IPv4 Addressing

**Structure:**

IPv4 addresses are 32-bit binary numbers, divided into four octets.
Each octet is represented in decimal format and separated by periods (e.g., 192.168.1.1).

**Classes:**

Class A: 1.0.0.0 to 126.255.255.255 (Default subnet mask: 255.0.0.0)

Class B: 128.0.0.0 to 191.255.255.255 (Default subnet mask: 255.255.0.0)

Class C: 192.0.0.0 to 223.255.255.255 (Default subnet mask: 255.255.255.0)

Class D: 224.0.0.0 to 239.255.255.255 (Multicast)

Class E: 240.0.0.0 to 255.255.255.255 (Experimental)

**Subnetting:** Subnetting divides a network into smaller networks (subnets).

**CIDR Notation:** Specifies the network address and the subnet mask (e.g., 192.168.1.0/24).

**Calculations:**

*Subnet Mask:* Determines the network and host portions of an IP address.

*Number of Subnets:* 2^number of subnet bits

*Number of Hosts per Subnet:* 2^number of host bits - 2

**Private IP Ranges:**

Class A: 10.0.0.0 to 10.255.255.255

Class B: 172.16.0.0 to 172.31.255.255

Class C: 192.168.0.0 to 192.168.255.255

**Subnetting Example:** 

Given IP: 192.168.10.0/24
Subnet Mask: 255.255.255.0

Number of Subnets: If we borrow 2 bits for subnetting: 2^2 = 4 subnets
Number of Hosts per Subnet: 2^6 - 2 = 62 hosts

### IPv6 Addressing

**Structure:**

IPv6 addresses are 128-bit binary numbers, represented in hexadecimal and separated by colons (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334).
Can be abbreviated by omitting leading zeros and using double colons (::) to represent consecutive groups of zeros (e.g., 2001:db8:85a3::8a2e:370:7334).

**Types of IPv6 Addresses:**

*Global Unicast:* Routable on the internet, starts with 2000::/3

*Link-Local:* Used within a single link, starts with fe80::/10

*Unique Local:* Used within a private network, starts with fc00::/7

*Multicast:* One-to-many communication, starts with ff00::/8

*Anycast:*  One-to-nearest communication

**Address Format:**

*Global Unicast Address:*
Prefix: First 48 bits (e.g., 2001:0db8::/48)
Subnet: Next 16 bits (e.g., 0001)
Interface ID: Last 64 bits (e.g., 0000:0000:0000:1)

*IPv6 Prefix Length:*
Similar to CIDR notation in IPv4 (e.g., /64).

*IPv6 Address Assignment:*
Stateless Address Autoconfiguration (SLAAC): Automatically configures IP addresses without a DHCP server.

**DHCPv6:** Configures IP addresses using a DHCP server.

**IPv6 Address Example:**

*Full Address:* 2001:0db8:0000:0042:0000:8a2e:0370:7334

Compressed Address: 2001:db8:0:42::8a2e:370:7334

**Subnetting in IPv6:**

Subnetting is simpler in IPv6 due to the large address space.

Subnet Example: 2001:db8:abcd::/64

Subnets: Can be divided into smaller subnets by extending the prefix (e.g., /65, /66).
