# Introduction

You and I have computers, smartphones, tablets, smart TVs, and even smartwatches.

These are devices that can work on their own and do something. When you connect them to the internet, via a 5G/4G connection, a Wi-Fi network, or by plugging in an Ethernet cable, you have access to the outside world.

Under the hood, when your device is connected to the internet, it’s assigned an IP address.

This is composed of 4 sets of numbers, from 0 to 255. You can find this number in the network settings of your device.

For example, the IP address of my MacBook now is `192.168.1.105`. Addresses that start with `192.168.` are reserved for local networks. That’s **your** local network.

The local network is created by your Wi-Fi/Ethernet router. The router is the device that’s connected to the internet provider.

This is what happens: the router connects to the internet provider and gets its own IP address.

Then the router creates the local network and assigns every device that connects to it a different local IP address. So every device in your house has a different IP address.

You can communicate between devices on your local network, but you cannot communicate with devices in _other_ local networks, for example, the ones in your friend’s house, unless things are set up for this.

This is because there is a level of protection. In a local network, the IP address is _private_.

Our devices can talk to the internet when they want, but the internet can’t talk to your devices unless you want it to and set up systems to do so (and this is by design, so you don’t have to spend the evening fighting hackers trying to set the room temperature of your smart thermostat, or worse).

So, we can tell our devices to talk to something on the internet. Cool. But… _who do we talk to?_

The answer is **other computers**. **Servers**, to give them a proper name.

A server is a computer whose job is to **serve us something**.

A server has an IP address, too.

This time, the IP address is **public** because the server is created to be reached, unlike our home devices. The server has to be reachable all the time.

A server also has a name, which we call a **domain name**.

_Other computers_, called DNS servers, have the job of mapping a domain name to an IP address. So instead of saying “visit `142.250.184.78` ” we say “visit google.com”.

Humans work best with names, computers work best with numbers. DNS makes it all very easy for both.

You don’t usually try to reach for a website using its IP address. You _can_, but it’s very rare.

You usually use a **domain name**. Like [google.com](http://google.com/), or [docs.dresume.me](http://docs.dresume.me/).

This is very handy because for example I can change the server location and company I use to host a website, while maintaining the same domain name.

The system that maps domain names to IP addresses is called DNS: **Domain Name System**.

The _language_ that computers use to talk to each other is called a **protocol**. The protocol that powers the internet we all know is called **Internet Protocol Suite**, also known as **TCP/IP**.

The IP protocol part is what I mentioned above; IP addresses and so on. That’s the base layer that identifies how computers can find each other.

On top of that layer, we have what we call **transport protocols**. They define how computers send packets of data to each other.

**TCP**, also known as **Transmission Control Protocol**, is one of them. This protocol makes sure packets are delivered from the client to the server, and from the server to the client.

We also have the **UDP** protocol, which is similar but different, we’ll see more about this later

I think we have the basics in place: **devices**, **IP addresses**, **and the TCP/IP protocol** that makes sure data can flow between computers.
