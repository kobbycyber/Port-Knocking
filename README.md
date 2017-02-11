# Port-Knocking
Reverse Port Knocking Shell


The backdoor runs forever to hack into the server, listens passively for incoming packets. 
The backdoor uses raw sockets for this purpose.

The Knocker is a client which issues the sequence of packets.

When the right sequence of packets arrive, the backdoor reaches out to a web server to fetch a linux command and executes it locally.
