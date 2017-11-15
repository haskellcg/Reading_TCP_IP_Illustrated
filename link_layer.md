  The purpose of the link layer in the TCP/IP protocol suite is to send and receive :
  * IP datagram for the IP module
  * ARP requests and replies for the ARP module
  * RARP requests and replies for the RARP module
  
## Ethernet and IEEE 802 Encapsulate
  **CSMA/CD (Carrier Sense, Multiple Access with Collision Detection)**  
  802.3 covers an entire set of CSMA/CD network   
  802.4 covers token bus network  
  802.5 covers token ring network  
  Common to all three of these is the 802.2 standard that defines the logical link control (LLC) common to many of the 802 network.  
  
  In the TCP/IP world, the encapsulation of IP datagrams is defined in **RFC 894** for Ethernet and in **RFC 1042** for IEEE 802 network. The Host Requirements RFC requires that every Internet host connected to a 10 Mbits/sec Ethernet cable:
  * Must be able to send and receive packets using RFC 894 (Ethernet) encapsulation.
  * Should be able to receive RFC 1042 (IEEE 802) packets intermix with RFC 894 packets.
  * May be able to send packets using RFC 1042 encapsulation. If the host can send both types of packets, the type of packets send must be configurable and the configuration option must default to RFC 894 packets.
  
  
