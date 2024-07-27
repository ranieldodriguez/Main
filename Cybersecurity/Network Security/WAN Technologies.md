# Point-to-Point Protocol (PPP):
## Commands:
    
    encapsulation ppp: Configures the interface to use PPP encapsulation.
    
    ppp authentication [chap|pap|mschap]: Configures PPP authentication methods.

# Frame Relay:

## Commands:
    
    encapsulation frame-relay: Configures the interface to use Frame Relay encapsulation.
    
    frame-relay map [protocol] [address] [dlci] broadcast: Maps a protocol address to a DLCI.
    
    frame-relay interface-dlci [dlci]: Configures the interface DLCI.

# VPNs (Virtual Private Networks):

### GRE (Generic Routing Encapsulation):
Encapsulates a wide variety of network layer protocols inside point-to-point connections.

### IPSec (Internet Protocol Security):
Provides secure communication over IP networks through authentication and encryption.

### DMVPN (Dynamic Multipoint Virtual Private Network):
Allows for the creation of dynamic, scalable VPNs.

# MPLS (Multiprotocol Label Switching)

**Commands**

    mpls ip: Enables MPLS on an interface.
    mpls label protocol [protocol]: Specifies the label distribution protocol.
    mpls ldp router-id [router-id]: Sets the LDP router ID.
    mpls traffic-eng tunnels: Enables MPLS traffic engineering tunnels.

# Metro Ethernet and Carrier Ethernet
E-LINE (Ethernet Line Service) and E-LAN (Ethernet LAN Service).

**Commands**

    ethernet service instance [number]: Configures an Ethernet service instance.
    encapsulation dot1q [vlan-id]: Specifies VLAN encapsulation.
    rewrite ingress tag [push|pop|translate]: Configures tag manipulation for VLANs.
