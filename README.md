# tcpdumpDNS

Using some examples to traceroute several websites...

Traceroute:
It shows the path of the packets that access network to reach the destination on the 
network when it finds a path. Running traceroute, it requires IP address and if I give 
a website name, it is replacing the the website name to IP address. On each line, there 
is a router's IP packet. Also, on each line, there is a time in milliseconds to each 
router or hop including its domain name or its IP address. 

When tracking the route to a domain name, it shows me an output that describes the following: 
-The IP address of that domain name, and tells if that domain name has multiple address, 
-The hop's maximum number before it times out and it can be increased if I give it with the 
"-m" option 
-Then print each router's IP that has been passed through the network to the destination.
-The default of packet length is 40 byte packets.
-Each router is tested 3 times or has three round trip times in milliseconds. 
By default after 5 seconds, there is no response, and asterisk is printed. 
The time can be increased to wait for a response with the "-w" option.
-In the network path, there are routers between the source and the final destination.

However, sometimes there was time out when the router did not respond and the path needs 
to try another router either it is successful or continuing as time out. 
When the packet was arrived at the destination, but there were one or two asterisks on 
router, it does not mean the packet was lost. Most fairways block ping or traceroute packets,
to prevent routers from being attacks.


There are some reasons when it shows three asterisks at end of the 
traceroute: 
The firewall and other security device block and prevent my request to the destination 
through using traceroute because the destination can be reached using a different 
application such as using the browser.
It could be a connection problem and the destination could not be reached. 


It uses time to live protocol on IP to return ICMP time exceeded in-transit. 
When I enter a domain name or IP address, it routes through different location
(cities and countries) around the world. Thus, routes tracked travel through many hops 
and it is depending on location, it travels through different ISPs regional internet 
registries (RIR). First the path depends on the owner of the router that belongs to 
the host's LAN, the company's owner, and depends on the route tables. Thus, the packet 
follow internal host 


Interesting, it does not work if there is only one router; for example, I tried to 
traceroute between my client and my server or between my internal network addresses 
on the part2, and it does not show to me any hops. It does not work if there is only 
one router in the network. Traceroute shows only pathes from the source to the destination 
but it does not print the path from the destination to the source. It prints lists of
each router's IP address that is in each individual routes. I can define routing problems 
in network when I trace IP address and see how far a packet that can travel 
through the network.
Surprise me: when the packet travels so far through a physical distance. The length of 
the longest possible path traveled between two point. 
 

Tcpdump:
I used tcpdump to capture packets. Using it with traceroute, it shows and match 
the network path. Tcpdump gives better detail and information of the issue such as if 
the issue is a firewall issue or a connection issue. It shows what port is currently 
being used. I can use a port to filter the traffic on tcpdump. 

I used tcpdump to capture packets. Using it with traceroute, it shows and match the network
path. Tcpdump gives better detail and information of the issue such as if the issue is a
firewall issue. The connection is coming from the source IP address
I tried some options of tcpdump.
-v, -vv or -vvv shows more informations, and each -v shows more details of information
-w: to write packet information to file or to standard output
-X: show the hex and ASCII text
-n: when it display, it dose not convert addresses to name. -nn, it does not convert
port to name.

> tcpdump -Xvr uba.pcap proto 1
to print the data in the file named uba.pcap and proto 1 filters it for ICMP and 17 for UDP


> grep UDP /etc/protocols
udp	17	UDP		# user datagram protocol
udplite	136	UDPLite		# UDP-Lite [RFC3828]


Stevens.edu:
There was 14 hops and the packet travels from the source (NetBSD system) to the destination 
(stevens.edu). Interesting, I also ran traceroute to one of the IP addresses in the output 
of the command, and it shows it is an unreachable destination because the router’s firewall
forwards the incoming traffic on some ports but it is blocked for incoming traffic if that 
router is used as a destination. Very common blocking ports as ICMP and UDP due to security.


from following output:

On tracroute there is three round trip times in milliseconds. The first line shows,
the first hop (216.182.224.76) has tested 3 times. On tcpdump shows more information such 
protocol and DNS name. 
The second hop, there were 3 different IP addresses and each IP address has its round 
trip time. ICMP can tell us if there is an issue with the connection 

ip-172-31-11-137# tcpdump -Xr stevens.pcap proto \\icmp


reading from file stevens.pcap, link-type EN10MB (Ethernet)
02:24:39.108512 IP 216.182.224.76 > ip-172-31-11-137.ec2.internal: ICMP time exceeded in-transit, length 36
	0x0000:  4500 0038 20a1 4000 ff01 ea77 d8b6 e04c  E..8..@....w...L
	0x0010:  ac1f 0b89 0b00 dd22 0000 0000 4500 0028  ......."....E..(
	0x0020:  c609 0000 0111 56d0 ac1f 0b89 6810 7d33  ......V.....h.}3
	0x0030:  c608 829b 0014 cf24                      .......$
02:24:39.112904 IP 216.182.224.76 > ip-172-31-11-137.ec2.internal: ICMP time exceeded in-transit, length 36
	0x0000:  4500 0038 20a3 4000 ff01 ea75 d8b6 e04c  E..8..@....u...L
	0x0010:  ac1f 0b89 0b00 efc3 0000 0000 4500 0028  ............E..(
	0x0020:  c60a 0000 0111 56cf ac1f 0b89 6810 7d33  ......V.....h.}3
	0x0030:  c608 829c 0014 bc82                      ........
02:24:39.113899 IP 216.182.224.76 > ip-172-31-11-137.ec2.internal: ICMP time exceeded in-transit, length 36
	0x0000:  4500 0038 20a5 4000 ff01 ea73 d8b6 e04c  E..8..@....s...L
	0x0010:  ac1f 0b89 0b00 f543 0000 0000 4500 0028  .......C....E..(
	0x0020:  c60b 0000 0111 56ce ac1f 0b89 6810 7d33  ......V.....h.}3
	0x0030:  c608 829d 0014 b701                      ........
02:24:39.115516 IP 100.64.8.55 > ip-172-31-11-137.ec2.internal: ICMP time exceeded in-transit, length 36
	0x0000:  4500 0038 3d2f 4000 fe01 1b76 6440 0837  E..8=/@....vd@.7
	0x0010:  ac1f 0b89 0b00 fa60 0000 0000 4500 0028  .......`....E..(
	0x0020:  c60c 0000 0111 56cd ac1f 0b89 6810 7d33  ......V.....h.}3
	0x0030:  c608 829e 0014 b1e3                      ........



Example, traceroute domainName
    
    
In the examples

www.stevens.edu and www.marburg.de
On Stevens: there was an IP address of router that is located 
in Los Angeles before reached to stevens.edu. As I mentioned the network path depends on
the owner of the company that provides the internet.
On marburg: at the middel hop 15, there were asterisks and that could be normal. 
However they were successful 

www.du.edu, www.usyd.edu.au
The round trip times got higher to around 200 mis range at the middel hop. This could 
be network level issue, there was a problem between two routes in the network, or 
the traffic could be overcrowding.
However, on usyd.edu.au, it reached the destination. 

www.hku.hk, www.uba.ar, www.du.edu, and www.hawaii.edu
At the final router there were asterisks are because of a firewall blocking traceroute packets.
Because I can reached the website through the browser. 

Visual Trace Route is in the USA:
I can trace from my location (proxy trace) or their location (host trace).
du.ac.in before reached the destination, it goes from my computer through many comcast's
routers in several location in the USA, then travels to Switzerland then to England.
It travels through different ISPs regional internet registries (RIR) 
when I trace uba.ar it shows the domain is an invalid address because the top-level 
domain "ar" could not recognize on Visual Trace Route website.


traceroute is in Germany:
It shows me when someone, who is from Germany, wants to access stevens.edu, 
First it goes to New York then Los Angeles before reached to the destination because the 
traffic travel through a global network from Europe to USA
du.ac.in is not reachable using this website. 
There is an issue when I trace uba.ar, I think because in the website there is buffering 
the data in memory 

These tools are useful when I need to test a website that is unreachable. I can find out 
where the connection fails. It is a good idea to save a traceroute and tcpdump file of 
my website during it is working because when it fails or is unreachable, I can compare these files.
Even if the path passes different network but it would be similar. 
Also if there was timed out after the first line, I would need to connect the company that 
provides internet services or the network admin because there was a problem 




