#Port-Knocking
Reverse Port Knocking Shell

##Description:
The backdoor runs forever to hack into the server, listens passively for incoming packets. 
The backdoor uses raw sockets for this purpose.

The Knocker is a client which issues the sequence of packets.

When the right sequence of packets arrive, the backdoor reaches out to a web server to fetch a linux command and executes it locally.

##Details:

###1.knocker

The knocker takes two arguments, a configuration file and an ip address. The Ip address is the address of the backdoor.

The knocker sends UDP packets to the backdoor on the ports sequence specified in the configuration file.

###2.Backdoor

*The backdoor is listening passively to all incoming packets. It uses raw socket and does not listen to any specific port. 

*The packet received is unpacked using the struct module and the destination port of the received packet is determined.

*The list of ports mentioned in the configuration file is maintained in a list named portlist.

*The source address and the destination port of the received packet is then sent as argument to the update function which updates the values in the map named pktmap.

*The update function checks for the position of the port in the portlist, and updates the pktmap accordingly.

*The verifier function checks if the value of the key in pktmap is equal to the length of portlist and fetches the command from the url and executes it.


For example if Configuration file has the sequence 2000, 2001, 2002

portlist will be [2000,2001,2002]

Thus when the function update receives a packet from 127.0.0.1 with port as 2000, it checks for its position in the portlist.
The position is 0. So the value stored for the Ip address is 1.
Next when it receives the packet from the same IP with port 2001, the position in portlist is 1, 
and also count is 1. So the update function adds 1 to the value, 
and so on.
The value will be 3 in pktmap when the verifier is called.

When the verifier function is called it checks if the value of the key in pktmap is equal to the length of portlist.
the value will be 3 in the above example when packets are received in the sequence.

And thereafter it will fetch the command from the url and execute it.
After this the values in the map are reset.


