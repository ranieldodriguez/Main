# **Cisco IOS Commands:**
  
  *show ip interface brief*: Displays a summary of the IP addresses and status of all interfaces on a router or switch.
  
  *show running-config*: Displays the current configuration running on the device.
  
  *show version*: Provides information about the Cisco IOS version, system uptime, and hardware details.
  
  *show ip route*: Displays the routing table of the router.
  
  *show interfaces*: Displays detailed information about all interfaces on the device.
  
  *configure terminal*: Enters global configuration mode from privileged EXEC mode.
  
  *interface [type] [number]*: Enters interface configuration mode for a specified interface (e.g., interface GigabitEthernet 0/1).
  
  *ip address [address] [mask]*: Assigns an IP address and subnet mask to an interface.
  
  *no shutdown*: Enables an interface (brings it up).
  
  *hostname [name]*: Sets the device's hostname.
  
  *enable*: Enters privileged EXEC mode from user EXEC mode.

*copy running-config startup-config*: Copies the running configuration to the startup configuration, saving changes.

# **Switching Concepts:**

**VLANs**: Virtual LANs separate network traffic logically without physical separation.

**VTP (VLAN Trunking Protocol)**: Manages VLAN configurations across multiple switches.

**DTP (Dynamic Trunking Protocol)**: Negotiates trunking on a link between two switches.

**STP (Spanning Tree Protocol)**: Prevents loops in network topologies.

**RSTP (Rapid Spanning Tree Protocol)**: Faster version of STP.

**EtherChannel**: Combines multiple physical links into one logical link for redundancy and increased bandwidth.

**Port Security**: Limits the number of MAC addresses on a switch port.

# **Routing Concepts:**

**Static Routing**: Manually configured routes.

**Dynamic Routing**: Automatically adjusts routes based on network changes.

**RIP (Routing Information Protocol)**:

  Distance vector protocol with a maximum hop count of 15.

    **Commands:**
      
      *router rip*: Enters RIP configuration mode.
      
      *network [network]*: Specifies networks to advertise.
      
      *version 2*: Enables RIP version 2.
      
      *no auto-summary*: Disables automatic summarization.
  

**EIGRP (Enhanced Interior Gateway Routing Protocol)**:

Advanced distance vector protocol using the DUAL algorithm.

    **Commands**:
    
      *router eigrp [AS number]*: Enters EIGRP configuration mode for a specific autonomous system.
      
      *network [network]*: Specifies networks to advertise.
      
      *no auto-summary*: Disables automatic summarization.
  
  
**OSPF (Open Shortest Path First)**:

Link-state protocol using Dijkstra’s algorithm.

    **Commands**:
      
      *router ospf [process ID]*: Enters OSPF configuration mode.
      
      *network [network] area [area ID]*: Specifies networks to advertise and associates them with an OSPF area.
