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
W  
## TCP/IP layering
  TCP and UDP are the predominant transport layer protocols. Both use IP as the network layer.  
  
  IP is the main protocol at the network layer. It is used by both TCP and UDP. Every piece of TCP and UDP data that get transfered around an internet goes through the IP layer at both system and at every intermediate router.  
  
  ICMP is an ajunct to IP. It is used by the IP layer to exchange error messages and other vitalinformation with IP layer in another host ot router. Ping and   Traceroute both use ICMP. 
  
  IGMP is the Internet Group Management Protocol. Is it used with multicast: sending a UDP datagram to multiple host.
  
  ARP (Address Resolution Protocol) and RARP (Reverse Address Resolution Protocol) are specialized protocols used only with centain types of network interfaces (such as Ethernet and token ring) to convert between the addresses used by the IP layer and the addresses used by the network interface.
  
## Internet Addresses
  Every interface on an internet must have a unique Internet address (also called an IP address).
  
  Classes|Bit|Range
  -------|---|-----
  A|0xxx.xxxx.xxxx.xxxx|0.0.0.0 ~ 127.255.255.255
  B|10xx.xxxx.xxxx.xxxx|128.0.0.0 ~ 191.255.255.255
  C|110x.xxxx.xxxx.xxxx|192.0.0.0 ~ 223.255.255.255
  D|1110.xxxx.xxxx.xxxx|224.0.0.0 ~ 239.255.255.255
  E|1111.xxxx.xxxx.xxxx|240.0.0.0 ~ 255.255.255.255
  
  The authority is the Internet Netwok Information Center, called the InterNIC.
  
  There are three types of IP address:
  * unicast (destined for a single host)
  * broadcast (destined for all hosts on a given network)
  * multicast (destined for a set of hosts that belong to a multicast group)

## The Domain Name System
  DNS is a distributed database that provides a mapping between IP and address and hostnames.
  
## Encapsulation
  Each layer adds information to the data by prepending headers (and sometimes adding trailer information) to the data that it receives:
  * The unit of data that TCP sends to IP is called a TCP **segment**
  * The unit of data that IP sends to the network interface is called a IP **datagram** (**packet**)
  * The stream of bits that flows across the Ethernet is called a **frame**
  
  A physical property of an Ethernet frame is that the size of its data must be **between 46 and 1500 bytes**.
  
  TCP, UDP, ICMP, IGMP all send data to IP. IP handles this by storing an 8-bit value in its header called **the protocol field**. A value of 1 is for ICMP, 2 is for IGMP, 6 indicates TCP, and 17 is for UDP.
  
  Both TCP and UDP use **16-bit port numbers** to identify applications. TCP and UDP store the source port number and destination port number in their respective headers.
  
  The network interface sends and receives frames on behalf of IP, ARP and RARP. There musst be some form of identification in the Ethernet header indicating which network layer protocol generated data. To handle this there is a 16-bit frame type field in the Ethernet header.
  
## Demultiplexing
  When an Ethernet frame is receive an the destination host, it starts its way up the protocol stack and all the headers are removed by the approperiate protocol box. This is called demultiplexing.
  
  Each protocol box looks at centain identifiers in its header to determine which box in the next upper layer receives the data.
  
## Client-Server Model
  We Can categories servers into two classes: iterative and concurrent.
  
  An iterative server iterates through following steps:
  1. wait for client request to arrive
  1. process the client request
  1. send the response back to the client that sent the request
  1. go back to step 1
  
  A concurrent server, on the other hand, performs the following steps:
  1. wait for a client request to arrive
  1. start a new server to handle this client's request. This may involve creating a new process, task, or thread, depending on what the underlying operating system supports. How this step is performed depends on the operating system. 
  1. go back to step 1
  
  As a general rule, TCP servers are concurrent, and UDP servers are iterative.
