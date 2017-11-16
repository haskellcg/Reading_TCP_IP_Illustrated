  IP is the workhorse protocol of the TCP/IP protocol suite. All TCP, UDP, ICMP, IGMP data gets transmitted as IP datagrams. IP provides an **unreliable**, **connectless** datagram delivery service.
  
  When something goes wrong, such as a router temporarily running out of buffers, IP has a simple error handling algorithm: throw away the datagram and try to send an ICMP message back to the source.
  
  The term connectionless means that IP does not maintain any **state information** about successive datagrams. Each datagrams is handled **independently from all other datagrams**. This also means that IP datagrams can get delivered out of order.

## IP Header
  [IP Header]()  
  
  The normal size of the IP header is 20 bytes, unless options are presents.
  
  The 4 bytes in the 32-bit value is transmitted **in the order**. This is called **big-endian byte ordering**, which is the byte ordering required for all binary integers in the TCP/IP headers as they traverse a network. This is called **the network byte order**. Machines that store binary intergers in other formats, such as the little endian format, must **convert the header values** into the network byte order before transmitting data.
  
  The _current version_ is 4, so IP is sometimes called IPv4.
  
  The _header length_ is the number of 32-bit words in the header, including any options. Since this is a 4-bit field, it limits the header **to 60 bytes (15 * 32 / 8 = 60)**. So the normal value of this field is 5.
  
  The _type of service_ field (TOS) is **composed of a 3-bit precedence field (which is ignore today), 4 TOS bits, and an unused bit that must be 0**. The 4 TOS bits are: minimize delay, maximize throughput, maximize reliability, and minimize menotary cost. **Only 1 of these 4 bits can be turned on**.    
  [recommended value for type of service]()  
  The TOS feature is not supported by most TCP/IP implementations today.
  
  The _total length_ field is the **total length of the IP datagram in bytes**. Using this field and the header length field, we know where the data portion of the IP datagram starts, and its length. This field also **changes when a datagram is fragmented**.  
  Although its possible to send a 65536-byte IP datagram, most link layers will fragment this. Reallistically, most implementations today allow for just over 8192-byte IP datagram.  
  The total length field is required in the IP header since some data links pad small frames to be a minimum length. Even though the minimum Ethernet frame size is 46 bytes, an IP datagram can be smaller. If the total length field wasn't provided, the IP layer wouldn't know how much of a 46-byte Ethernet frame was really an IP datagram.
  
  The _identification_ field uniquely identifies each datagram sent by a host. It normally increments by one each time a datagram is sent. 
  
  The _flags_
  
  The _fragment offset_
  
  The _time-to-live_ field, or TTL, sets an **upper limit on the number of routers** through which a datagram can pass. It limits the lifetime of the datagram. It is initialized by the sender to some values (often 32 or 64) and decrement by one by every router that handles the datagram. When this field reaches 0, the datagram is throw away, and the sender is notified with an ICMP message. This prevents packets from getting caught in routing loop forever.
  
  The _protocol_ 
  
  The _header checksum_ is calculated for outgoing datagram, the value of the checksum is first set to 0. Then the 16-bit one's complement sum of the header is calculated (i.e. the entire header is considered a sequence of 16 bit words).  
  Since the receiver's calculated checksum contains the checksum stored by the sender, the receiver's checksum is all one bits if nothing in the header was modified. If the result is not all one bit (a checksum error), IP discard the received datagram.  
  ICMP, IGMP, UDP and TCP all use the same checksum algorithm, although TCP and UDP include various field from the IP header, in addition to their own header and data.  
  Since a router often changes only the TTL field (decrementing it by 1), a router can incrementally update the checksum when it forwards a receive datagram, instead of calculating the checksum over the entire IP header again.
  
  The _source IP address_
  
  The _destinition IP address_
  
  The _options_ is a variable-length list of optional informaion for the datagram:
  * security and handling restrictions (for military applications)
  * record route (have each route record its IP address)
  * timestamp (have each route record its IP address and time)
  * loose source routing (specifying a list of IP addresses that must be travered by the datagram)
  * strict source routing (similar to loose source routing but here only the addresses in the list can be traversed)  
  These options are rarely used and not all host and routers support all the options.  
  **The options field always ends on a 32-bit boundary. Pad bytes with a value of 0 are added if necessary. This assure that IP header is always a multiple of 32 bit (as required for the _header length_ field)**
