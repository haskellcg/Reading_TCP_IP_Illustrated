  The TCP/IP protocol suite allows computers of all sizes, from many different computer vendors, running totally different operating systems, to communicate with each other.  
  
## Layering
  Networking protocols are normally developed in layers, with each layers responsible for a different facet of the communications.  
  
  TCP/IP is normally considered to be a 4-layer system:
  * The link layer, sometimes called the **data-link layer** or **network interface layer**, normally includes **device driver** in the operating system and the corresponding **network interface card** in the computer. Together they handle all the **hardware details of physically interfacing** with the cable (or whatever type of media is being used).
  * The network layer, sometimes called **internet layer**, handles the **movements of packets** around the network. **Routing of packets**, for example, takes place here. IP (Internet Protocol), ICMP (Internet Control Message Protocol), and IGMP (Internet Group Management Protocol) provide the network layer in the TCP/IP protocol suite.
  * The transport layer provides **a flow of data** between two hosts, for the application layer above. In the TCP/IP protocol suite there are two vastly different transport protocols: TCP (Transmission Control Protocol) and UDP (User Datagram Protocol). TCP provides a **reliable flow of data** between hosts. It is concerned with things such as dividing the data passed to it from the application into **appropriately sized chunks for the network layer** below, **acknowledging received packets**, setting timeouts to make certain the other end acknowleges packets that are sent.
  * The application layer handles the details of the particular application: 
    * Telnet for remote login
    * FTP, the file transfer Protocol
    * SMTP, for electronic mail
    * SNMP, the Simple Network Management Protocol
    
  The easiest way to build an internet is to connect two or more networks with **router (IP router)**. The nice thing about routers is that they provide **connections to many different types of physical network**: Ethernet, token-ring, point-to-point , FDDI (Fiber Distributed Data Interface), and so on.    
  Gateway is used for application gateway: a process that **connect two different protocol suits** for one particular application.
  
  A router, by definition, has two or more network interface layer. Any system with multiple interface is called **multihomed**. Most TCP/IP implementations allow a multihomed host to act as a router also, but the host need to be specially configured for this to happen.
  
  Another way to connect networks is with **bridge**. These connect network at the link layer, while routers connect networks at the network layer. Bridges makes multiple LANs appears to the upper layers as a single LAN.
  
## TCP/IP layering
  TCP and UDP are the predominant transport layer protocols. Both use IP as the network layer.  
  
  IP is the main protocol at the network layer. It is used by both TCP and UDP. Every piece of TCP and UDP data that get transfered around an internet goes through the IP layer at both system and at every intermediate router.  
  
  ICMP is an ajunct to IP. It is used by the IP layer to exchange error messages and other vitalinformation with IP layer in another host ot router. Ping and   Traceroute both use ICMP. 
  
  IGMP is the Internet Group Management Protocol. Is it used with multicast: sending a UDP datagram to multiple host.
  
  ARP (Address Resolution Protocol) and RARP (Reverse Address Resolution Protocol) are specialized protocols used only with centain types of network interfaces (such as Ethernet and token ring) to convert between the addresses used by the IP layer and the addresses used by the network interface.
  
## Internet Addresses
  Every interface on an internet must have a unique Internet address (also called an IP address).
  
  Classes
