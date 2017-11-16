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
  
## Trailer Encapculation
  **RFC 893** describes another form of encapsulation used on Ethernet, called **trailer encapsulation**.
  
## SLIP: Serial Line IP

It is a simple form of encapsulation for IP datagrams on serial lines, and is specified in **RFC 1055**. SLIP has become popular for connecting home systemsto the Internet, through the ubiquitous RS-232 serial port found on almost every computer and high-speed modems.
  
  The following rules specify the framing used by SLIP:
  * The IP datagram is terminated by the special character called END (0xc0). Also to prevent any line noise before this datagram from being interpreted as part of this datagram, most implementations transit an END character at the beginning of the datagram too.
  * If a byte of the IP datagram equals the END character, the 2-byte sequence **0xdb, 0xdc** is transmitted instead. This special character, 0xdb, is called the SLIP ESC character, but its value is different from ASCII ESC character (0x1b).
  * If a byte of the IP datagram equals the SLIP ESC character, the 2-byte sequence **0xdb, 0xdd** is transmitted.

## Compressed SLIP
  Since SLIP lines are often slow (19200 bits/sec or below) and frequently used for interactive traffic.
  
  CSLIP (Compressed SLIP) is specified in RFC 1144. CSLIP normally reduces the 40 byte header to 3 or 5 bytes. It maintains the state of up to 16 TCP connections on each end of the CSLIP link and knows that some of the field in the two headers for a given connection normally dont change.
  
## PPP: Point-to-Point Protocol
  PPP, the Point-to-Point Protocol, corrects all the deficiencies in SLIP.
  
  PPP consist of three components:
  * A way to encapsulate IP datagrams on a serial link. PPP supports either an asynchronous link with 8 bits of data and no parity (i.e., the ubiquitous serial interface found on most computers) or bit-oriented synchronous links.
  * A link control protocol (LCP) to establish, configure, and test the data-link connection. This allows each end to negotiate various options.
  * A family of network control protocols (NCPs) specific to different network layer protocols. RFCs currently exist for IP, the OSI network layer, DECnet, and AppleTalk.
  
  Since PPP, like SLIP, is often used across slow serial links, reducing the number of bytes per frame reduces the latency for interactive application. Using the link control protocol, most implementation negotiate to omit the constant address and control and to reduce the size of the protocol field from 2 bytes to 1 byte.
  
  In summary, PPP provides the following advantages over SLIP:
  * suport for multiple protocols on a single serial line, not just IP datagrams
  * a cyclic redundancy check on every frame
  * dynamic negotiate of the IP address for each end (using IP network control protocol)
  * TCP and IP headers compression similar to CSLIP
  * a link control protocol for negotiate data-link options
  
## Loopback Interface  
  Most implementation supports a loopback interface that allow a client and server on the same host to communicate with each other using TCP/IP. The **class A network ID 127** is reserved for the loopback interface.
  
  The key points to note in this figure are as follows:
  * Everything send to the loopback address (nromally 127.0.0.1) appears as IP input.
  * Datagrams sent to a broadcast address or a multicast are copied to the loopback interface and sent out on the Ethernet. This is because the definition of broadcasting and multicasting includes the sending host
  * Anything sent to one of the host's own IP address is sent to loopback interface.
  
  While it may seem inefficient to perform all the transport layer and IP layer processing of the loopback data, it simplifies the design because the loopback interface appears as just another link layer to the network layer. The network layer passes a datagram to the loopback interface like any other link layer.
  
  IP datagram sent to the one of the host's own IP address normally do not appear on the corresponding network.
  
## MTU
  there is limit on the size of the frame for both Enthernet encapsulation and 802.3 encapsulation. This limits the number of bytes of data to 1500 and 1492, respectively. This characteristic of the link layer is called the MTU, its maximum transmission unit.
  
  If IP has a datagram to send, and the datagram is larger than the link layer's MTU, IP performs **fragmentation**, breaking the datagram up into smaller pieces (fragments), so that each fragment is smaller than the MTU.
  
  Network|MTU(bytes)
  -------|----------
  Hyperchannel|65535
  16 Mbits/sec token ring (IBM)|17914
  4 Mbits/sec token ring (IEEE 802.5)|4464
  FDDI|4352
  Ethernet|1500
  IEEE 802.3/802.2|1492
  X.25|576
  Point-to-Point (low delay)|296
  
## Path MTU
  When two host on the same network are communicating with each other, it is the MTU of the network that is important.
  
  But when two host are communicating across multiple network, each link can have a different MTU. The smallest MTU of any data link that packets traverse between the two hosts is important, which is called **path MTU**.
  
  The path MTU between any two hosts need not to be contant. It depends on the route being used at any time.
  
  The path MTU need not to be the same in the two directions.
  
## Serial Line Thrroughput Calculations
  Most SLIP implementation do provides this type-of-service queueing, placing interactive traffic ahead of bulk data traffic. The interactive traffic is normally Telnet, Rlogin and the control portion of FTP.
  
  Human factors studies have found that an interactive response time longer than 100-200 ms is perceived as bad. This is round-trip time for an interactive packet to be sent and sometime to be returned.
  
  Reducing the MTU of the SLIP link to 256 means the maximum amount of time can be busy with single frame is 266 ms, and half of this is 133 ms. This is better, but still not perfect. The reason we choose this value is to provide good utilization of the line of bulk data transfer.
  
  Since the MTU is a value that IP queries the link layer for, the value must include the normal TCP and IP headers. This i how IP makes its fragmentation decision. IP knows nothing about the header compression that CSLIP performs.
  
  Out average wait calculation (one-half the time required to transfer a maximum sized frame) only applies when a SLIP link is used for both interactive traffic and bulk data transfer. When only interactive traffic is being exchanged, 1 bytes of data in each direction (assuming 5-byte compressed headers) take around 12.5 ms for the round trip at 9600 bits/sec. This is well within the 100-200 ms range mentioned earlier. Also notice that compressing the headers from 40 bytes to 5 bytes reduces the round-trip time for the 1 byte of data from 85 to 12.5 ms.
