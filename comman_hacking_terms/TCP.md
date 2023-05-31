#### TCP is connection-oriented -
- Before actually sending data to the destination host, the two hosts communicate to estaiblish a connection. Once the connection is estaiblished, the data exchange begins.

#### TCP provides reliable communication - 
- The destination host must acknowledge that it received each TCP segment.
- If a segment isn't acknowledged, it is sent again.

#### TCP provides sequencing - 
- Sequence numbers in the TCP header allow destination hosts to put segments in the correct order evern if they arive out of order.

#### TCP provides flow control - 
- The destination host can tell the source host to increase/decrease the rate that data is sent.![[TCP_header.png]]

# Three way handshake - 
syn flag - synchronization flag
ack flag - acknowledgement flag
![[tcp_three_way_handshake.png]]