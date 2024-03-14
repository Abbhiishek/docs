# The TCP protocol

TCP means **Transfer Control Protocol**, and it’s the basis of the Web and other applications like Email.

Defined in [RFC 793](https://tools.ietf.org/html/rfc793) in 1981, TCP is one of the oldest pillars of the Internet.

TCP sits on top of the Internet Protocol (IP).

Upon it, other application-level protocols like HTTP, FTP, IMAP (and many others) operate.

TCP, contrary to IP and UDP, is **connection oriented**.

Before transmission can happen over TCP, a connection must be established. Data is sent, in form of little packets, and when the communication ends the connection is closed.

When data is transmitted over TCP, there’s a relatively complex workflow called handshake that must happen.

I will not go into the details here, but this handshake allows the end-to-end connection to happen, and this makes sure TCP can provide one of its peculiar features: reliability. Using TCP, we can always know if a packet the sender sent was received correctly by the receiver.

If a packet gets lost, the protocol is able to handle it and the packet is re-sent.

On the IP protocol, connections happen from computer to computer. In TCP, a connection happens from process to process, using the concept of **ports**.

The port, associated to an IP address, allows to uniquely identify a process on a computer. Like this:

`localhost:8080`

or

`google.com:1234`

Each application protocol has a default port. For example HTTP has 80, HTTPS has 443 and FTP has 21. This is why you don’t usually have to specify the port, in the browser.

Programs are not required to use the default, this is why especially on your local computer, you might see ports like 1313 or 8080 when you start a new application.

Port numbers range from 1 to 65535 (the port number is a 16 bits unsigned, which corresponds to 2^16 possible values).
