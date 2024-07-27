# Cisco IOS Commands

    show ip protocols: Displays the status of all active routing protocols.
    show ip bgp: Displays BGP routing table information.
    show ip ospf: Displays general OSPF routing protocol information.
    show ip eigrp topology: Displays the EIGRP topology table.
    clear ip bgp [*|neighbor]: Resets BGP connections.
    clear ip route [*|network]: Clears routing table entries.
    
# Advanced Switching Concepts:

**VTP Versions and Modes**

*VTPv1, VTPv2, VTPv3*: Different versions with various capabilities.

*VTP Modes*: Server, Client, Transparent, and Off.

*Commands*

    vtp mode [mode]: Sets the VTP mode.
    vtp domain [name]: Sets the VTP domain.
    vtp version [version]: Sets the VTP version.
    vtp password [password]: Sets the VTP password.

**Private VLANs**:

Used to segregate traffic within a VLAN.

*Commands*

    private-vlan primary: Configures a VLAN as a primary VLAN.
    private-vlan association [secondary-VLAN]: Associates a secondary VLAN with a primary VLAN.

**StackWise and VSS (Virtual Switching System)**

*StackWise*: Allows multiple switches to operate as a single unit.

*Commands*:

    switch stack-member-number priority [priority]: Sets the priority of a switch within the stack.
    switch stack-member-number renumber [new-stack-member-number]: Changes the stack member number.

*VSS*: Combines two switches into a single logical switch for higher availability and scalability.

*Commands*:

    switch virtual domain [domain-id]: Configures the VSS domain.
    switch virtual link [link-id]: Creates a virtual link between VSS members.
    switch virtual mode enable: Enables VSS mode.

# Advanced Routing Concepts:

**BGP (Border Gateway Protocol)**
BGP Attributes: AS-PATH, NEXT-HOP, LOCAL_PREF, MED, etc.

*Commands*

    router bgp [AS-number]: Enters BGP configuration mode.
    neighbor [IP-address] remote-as [AS-number]: Configures a BGP neighbor.
    network [network] mask [mask]: Advertises a network in BGP.
    neighbor [IP-address] route-map [map-name] in|out: Applies a route map to a BGP neighbor.

**OSPF (Open Shortest Path First) Advanced Features**
OSPFv3 for IPv6, OSPF Multi-Area, OSPF Authentication.

*Commands*

    router ospf [process-id]: Enters OSPF configuration mode.
    area [area-id] range [network] [mask]: Configures OSPF area range.
    ip ospf authentication-key [key]: Configures OSPF simple password authentication.
    ipv6 router ospf [process-id]: Configures OSPFv3.

**EIGRP (Enhanced Interior Gateway Routing Protocol) Advanced Features**
EIGRP for IPv6, EIGRP Authentication, Named EIGRP Configuration.

*Commands*

    router eigrp [AS-number]: Enters EIGRP configuration mode.
    eigrp router-id [router-id]: Sets the EIGRP router ID.
    network [network]: Advertises a network in EIGRP.
    eigrp stub [stub-options]: Configures EIGRP stub routing.
    key chain [name]: Configures an EIGRP key chain for authentication.
    ipv6 router eigrp [AS-number]: Configures EIGRP for IPv6.
