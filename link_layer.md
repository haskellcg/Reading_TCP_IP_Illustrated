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
  
# PPP: Point-to-Point Protocol
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
  
## Lookback Interface
  
  * 
