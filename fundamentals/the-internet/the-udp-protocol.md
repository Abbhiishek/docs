# The UDP protocol

UDP, **User Datagram Protocol**, is a transfer protocol, an alternative to TCP.

Its main difference from TCP is that it’s connectionless.

This implies that it’s faster, each packet sent is more lightweight, as it does not contain all the information needed in TCP, and it does have a lighter handshake process.

The drawback is that UDP is not as reliable as TCP.

In TCP, if a packet gets lost, the protocol is able to handle it and the packet is re-sent.

In UDP, this is not built-in into the protocol, and must be handled at a higher level (built on top of it). There is no built-in check to control if a packet was received, and if it is received correctly.

UDP was defined in [RFC 768](https://tools.ietf.org/html/rfc768) in 1980.

Some of the most notable application protocols that rely on the UDP layer are [DNS](https://thevalleyofcode.com/the-internet/3-the-dns-protocol) and DHCP, and more importantly is the base layer of **HTTP/3**, the next version of HTTP.

The UDP protocol uses ports to allow communication between processes, like with TCP.
