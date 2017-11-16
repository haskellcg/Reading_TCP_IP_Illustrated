  IP is the workhorse protocol of the TCP/IP protocol suite. All TCP, UDP, ICMP, IGMP data gets transmitted as IP datagrams. IP provides an **unreliable**, **connectless** datagram delivery service.
  
  When something goes wrong, such as a router temporarily running out of buffers, IP has a simple error handling algorithm: throw away the datagram and try to send an ICMP message back to the source.
  
  The term connectionless means that IP does not maintain any **state information** about successive datagrams. Each datagrams is handled **independently from all other datagrams**. This also means that IP datagrams can get delivered out of order.
