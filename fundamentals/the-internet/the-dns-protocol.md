# The DNS protocol

You don’t usually try to reach for a website using its IP address. You _can_, but it’s very rare.

You usually use a **domain name**. Like google.com, or flaviocopes.com.

This is very handy because for example I can change the server and company I use to host a website, while maintaining the same domain name.

The system that maps domain names to IP addresses is called DNS: **Domain Name System**.

DNS is a network of servers. Your provider will have its own DNS, your router already preconfigured to use it.

You can also choose to use Google’s DNS server, which has the IP address `8.8.8.8`.

Those DNS servers will receive the requests from your computer, and in turn will ask their own reference DNS server.

The system is organized like a tree. There is one DNS server at the top, called **root DNS server**.

To simplify, it knows the IP address of the DNS servers that are managing each domain extension, like `com`, `net`, `org` and so on, including the country-specific domain extensions and the new ones like `blog`, `dev` or `tech`.

Those DNS servers know the IP addresses mapping of all the domains under their extension.

Of course the system is set up to ensure caching, redundancy and capacity to endure high concurrent requests, but this is the general idea.
