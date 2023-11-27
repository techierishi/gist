_Linux Network Command_
----------
1. `ifconfig` - ifconfig (interface configurator) command is use to initialize an interface, assign IP Address to interface and enable or disable interface on demand. With this command you can view IP Address and Hardware / MAC address assign to interface and also MTU (Maximum transmission unit) size.
    + interface name
    + mask
    + loopback address
- `ifconfig -a`
    + ifconfig with interface (eth0) command only shows specific interface details like IP Address, MAC Address etc. with `-a` options will display all available interface details if it is disable also.
- `ifconfig -v`
- `ifconfig -s`

- Assigning IP Address and Gateway: Assigning an IP Address and Gateway to interface on the fly. The setting will be removed in case of system reboot.
    + `ifconfig eth0 192.168.50.5 netmask 255.255.255.0`
- Enable or Disable Specific Interface: 
    + Enable eth0: `ifup eth0`
    + Disable eth0: `ifdown eth0`
- Setting MTU Size: By default MTU size is 1500. We can set required MTU size with below command. Replace XXXX with size.
    + `ifconfig eth0 mtu XXXX` 
- Set Interface in Promiscuous mode: Network interface only received packets belongs to that particular NIC. If you put interface in promiscuous mode it will received all the packets. This is very useful to capture packets and analyze later. For this you may require superuser access.
    + `ifconfig eth0 -promisc`
2. `PING` - PING (Packet INternet Groper) command is the best way to test connectivity between two nodes. Whether it is Local Area Network (LAN) or Wide Area Network (WAN). Ping use ICMP (Internet Control Message Protocol) to communicate to other devices. 
- `ping 4.2.2.2`
- `ping www.tecmint.com`
- In Linux ping command keep executing until you interrupt. Ping with -c option exit after N number of request (success or error respond).
    + `ping -c 5 www.tecmint.com`
3. `TRACEROUTE`: `traceroute` is a network troubleshooting utility which shows number of hops taken to reach destination also determine packets traveling path. Below we are tracing route to global DNS server IP Address and able to reach destination also shows path of that packet is traveling.
- `traceroute 4.2.2.2`
4. `NETSTAT`: `Netstat` (Network Statistic) command display connection info, routing table information etc. To display routing table information use option as `-r`.
- `netstat -r`
- Listing all ports (both TCP and UDP) using netstat -a option.
    + `netstat -a | more`
- Listing TCP Ports connections
    + `netstat -at`
- Listing UDP Ports connections
    + `netstat -au`
- Listing all active listening ports connections with `netstat -l`.
    + `netstat -l`
- Listing all active listening TCP ports by using option `netstat -lt`.
    + `netstat -lt`
- Listing all active listening UDP ports by using option `netstat -lu`.
    + `netstat -lu`
- Listing all active UNIX listening ports using `netstat -lx`.
    + `netstat -lx`
- Displays statistics by protocol. By default, statistics are shown for the TCP, UDP, ICMP, and IP protocols. The -s parameter can be used to specify a set of protocols.
    + `netstat -s`
- Showing Statistics by TCP Protocol
    + `netstat -st`
- Showing Statistics by UDP Protocol
    + `netstat -su`
- Displaying service name with their PID number, using option `netstat -tp` will display "PID/Program Name".
    + `netstat -tp`
- Displaying Promiscuous mode with `-ac` switch, netstat print the selected information or refresh screen every five second. Default screen refresh in every second.
    + `netstat -ac 5 | grep tcp`
- Display Kernel IP routing table with netstat and route command.
    + `netstat -r`
- Showing network interface packet transactions including both transferring and receiving packets with MTU size.
    + `netstat -i`
- Showing Kernel interface table, similar to `ifconfig` command.
    + `netstat -ie`
- Displays multicast group membership information for both IPv4 and IPv6.
    + `netstat -g`
- To get netstat information every few second, then use the following command, it will print netstat information continuously, say every few seconds.
    + `netstat -c`
- Finding un-configured address families with some useful information.
    + `netstat --verbose`
- Find out how many listening programs running on a port 
    + `netstat -ap | grep http`
- Displaying RAW Network Statistics
    + `netstat --statistics --raw`
5. `DIG`: Dig (domain information groper) query DNS related information like A Record, CNAME, MX Record etc. This command mainly use to troubleshoot DNS related query.
- `dig www.tecmint.com`
6. `NSLOOKUP`: nslookup command also use to find out DNS related query. The following examples shows A Record (IP Address) of tecmint.com.
- `nslookup www.tecmint.com`
- Find out `A` record (IP address) of Domain
    + `nslookup www.tecmint.com`
- Find out Reverse Domain Lookup(Non-authoritative answer: displays A record of www.yahoo.com)
    + `nslookup 209.191.122.70`
- Find out specific Domain Lookup
    + `nslookup ir1.fp.vip.mud.yahoo.com.`
- To Query MX (Mail Exchange) record.MX record is being used to map a domain name to a list of mail exchange servers for that domain. So that it tells that whatever mail received / sent to @yahoo.com will be routed to mail server.
    + `nslookup -query=mx www.yahoo.com`
- To query SOA (Start of Authority) record.
    + `nslookup -type=soa www.yahoo.com`
- To query all Available DNS records.
    + `nslookup -query=any yahoo.com`
- Enable Debug mode
    + `nslookup -debug yahoo.com`
7. `ROUTE`: `route` command also shows and manipulate ip routing table. To see default routing table in Linux, type the following command.
- `route`
- `Route Adding`: `route add -net 10.10.10.0/24 gw 192.168.0.1`
- `Route Deleting`: route del -net 10.10.10.0/24 gw 192.168.0.1
- `Adding default Gateway`: `route add default gw 192.168.0.1`
8. `HOST`: `host` command to find name to IP or IP to name in `IPv4` or `IPv6` and also query DNS records.
- `host www.google.com`
- Using -t option we can find out DNS Resource Records like CNAME, NS, MX, SOA etc.
    + `host -t CNAME www.redhat.com`
9. `ARP`: ARP (Address Resolution Protocol) is useful to view / add the contents of the kernel's ARP tables. To see default table use the command as.
- `arp -e`
10. `ETHTOOL`: `ethtool` is a replacement of mii-tool. It is to view, setting speed and duplex of your Network Interface Card (NIC). You can set duplex permanently in `/etc/sysconfig/network-scripts/ifcfg-eth0` with `ETHTOOL_OPTS` variable.
- `ethtool eth0`
11. `IWCONFIG`: `iwconfig` command in Linux is use to configure a wireless network interface. You can see and set the basic Wi-Fi details like SSID channel and encryption.
- `iwconfig [interface]`
12. `HOSTNAME`: `hostname` is to identify in a network. Execute hostname command to see the hostname of your box. You can set hostname permanently in `/etc/sysconfig/network`. Need to reboot box once set a proper hostname.
- `hostname`
13. GUI tool system-config-network: system-config-network in command prompt to configure network setting and you will get nice Graphical User Interface (GUI) which may also use to configure IP Address, Gateway, DNS etc.
