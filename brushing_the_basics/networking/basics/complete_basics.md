# Computer Networks

## Client Server Architecture

- A **client** is a machine that requests information from another machine which is called **server**
- 

## Protocols

- TCP (Transmission Control Protocol)
  - It ensures data is transferred uncorupped

- UDP (User Datagram Protocol)
  - If we don't care, if we recieve 100% of the data. Example - Video Conference data

- HTTP (HyperText Transfer Protocol)
  - It defines the format in which data will be consumed

## Addresses

- Computers on the internet are identified by IP Addresses
- Every domains. such as `google.com` are linked to an IP address
- Format of an IP Address: `X.X.X.X`; where `X` is a number between 0 and 255
- Some IP addresses are reserved
- To know your IP address (on Ubuntu): `curl ifconfig.me -s`

## ISPs and Modems

- ISP (Internet Service Providers) are companies that provides you devices to access the Internet. Example - AT&T, Vodafone
- They provide a Modem/Router which has a global IP address.
- The modem assigns IP to any device which gets connected to the modem. These are known as local IP addresses. This assignment of IP is done through DHCP (Dynamic Host Control Protocol)
- If we access any website from any one of the connected device, that website will only be able to see the global IP address
- Once the response is recieved from the website, the modem will use NAT (Network Access Translator) and see which device it has to send the response

## Ports

- As we saw above, the router can "route" the response from the website, to the specific device that made a request to that website.
- What if we want to send that response to a particular application, which made that request and is present on the device that response was routed to?
- This is done using **Ports**
- Basically, every application (on a device) runs on same IP address. **Ports** helps us to create a distinction between them
- Example: `172.12.3.3:3456`; where `3456` is the port number.
- These are 16-bit numbers. The total number of possible Ports are 65536.
- Well known Ports:
  - HTTP - 80
  - HTTPS - 443
- Reserverd Ports are between 0 and 1023

## Network Connection Types

- LAN 
  - It's restricted to a particular area
  - Ethernets, WIFI

- MAN (Metropolitan Area Network)
  - Accross the city

- WAN (Wide Area Network)
  - Accross countries
  - Optical Fiber cables

- All of these come together and form the internet.

## Network Topologies

- Bus Topology
  - Single Bus, all the computers are connected to it

- Ring Topology
  - All connected in a ring shape
  - Sending a message between two computers require the data to go through computers between these two

- Start Topology
  - One central device connected to all computers
  - If central device fails, the complete network breaks

- Tree Topology
  - Bus +_Start

- Mesh Topology
  - Every Single computer is connected to every single computer
  - Pretty expensive


## OSI (Open Systems Interconnection) Model

- Application Layer
  - It's the Software that users interact with

- Presentation Layer
  - It recieves the data from the application layer and converts them into binary format
  - It encrypts the data
  
- Session Layer
  - The session layer is responsible for establishing, maintaining, and terminating communication sessions between devices on a network.
  - It allows two devices to communicate with each other in a full-duplex mode
  - RPC and NetBIOS protocols operate at this level

- Transport Layer
  - Responsible for the transfer of data
    - Data recieved from Session layer, it is divided into smaller data units called segments
    - These segments will contain the source and destination port number, sequence number
    - TCP is connection-oriented transmission and UDP is connectionless-oriented transmission 

- Network Layer
  - The network layer is responsible for providing logical addressing and routing services for data transmission between devices on a network. It assigns unique logical addresses (also known as IP addresses) to each device on a network and uses these addresses to route data packets between devices
  - Protocols that operate here: IP, ICMP, IGMP


- Data Link Layer
  - Physical addressing (MAC addresses) is done here
  - MAC address is the address of the network interface of the PC

- Physical Layer
  - Hardware Layer
  - Transport 0s and 1s through cables


## TCP/IP Model

- Similar to OSI, with difference layers. It's used more today
- Layers:
  - Application
    - User interacts with this layer. These are browsers, applications (web or mobile)
    - Protocols: HTTP, DHCP, SMTP, SSH
  - Transport
  - Network
  - Data Link
  - Physical

### Application Layer

**Socket**

- It's like an interface between two devices, which facilitates the flow of data packets
- Usually, the server creates a socket on their end (say, at port 8080) and when the client the dails this port, it responds with some actions defined in the `handler` function which triggers upon a request recieved by the client on that socket

**Ephemeral Ports**

Ephemeral ports are temporary, unused port numbers that are assigned to a socket when a connection is established. They are used to provide a unique identifier for the connection between the two computers.

In a client-server model, the client typically initiates a connection to the server by sending a request to a well-known port number, such as 80 for HTTP or 25 for SMTP. The server responds to the request by establishing a connection to the client using an ephemeral port number. This ensures that each connection between the client and server can be uniquely identified by the combination of the client's IP address and port number, and the server's IP address and ephemeral port number.

Ephemeral port numbers are typically assigned from a range of port numbers that are reserved for this purpose. The range of ephemeral port numbers is typically between 1024 and 65535, although the specific range may vary depending on the operating system.

Ephemeral ports are used to allow multiple clients to connect to a server simultaneously, as each client can be assigned a unique ephemeral port number for its connection. When the connection is closed, the ephemeral port number is released and can be used for a new connection.

#### HTTP (Hyper Text Transfer Protocol)

- It lays down the standards for how the request and response should be.
- It has two transport protocols: TCP abd UDP
- **Methods**: These are instructions for server on what action to do once it gets the request from client. These are: GET, POST, PUT, DELETE
- **Status Codes**: It is recieved from server which tells the client the result of the response, whether it passed, failed or something.
  - It a 3 digit number and follows the below convention:
    - `1xx` - Informational
    - `2xx` - Success
    - `3xx` - Redirect
    - `4xx` - Client Error
    - `5xx` - Server Error

#### Cookies
- It's a unique string stored on client's browser by a website.
- So, if you visit that website again, it will get to know, from the cookie, that it's not my first visit to the website. Cookie is usually sent in the Request Header, and the field name is `set-cookie`.

#### DNS (Domain Name System)

- Every domain name has an IP address associated with it
- It's a basically a registry service
- **Root DNS Servers**:
  - These are the first point of contact while resolving a url
  - These store TLDs (Top Level Domains) such as `.com`, `.org`
  - Here you can see where the Root DNS Server Databases are located: `https://root-servers.org/`
  - ICANN (Internet Corpo for Assigned Names and Numbers) manages them

- What happens when I try to resolve `www.google.com`?
  - The first check is performed locally to see if there are any IP associated with `google.com` that was earlier stored in local cache.
  - If its not there in the local cache, it checks the Local DNS server (it's usually your ISP).
  - If its not present there, it checks in the Root Server

### Transport Layer

- It handles the transportation of information between the network and the application (Note: Network to Network transmission is handled in Network Layer)
- It takes care of congestion control in the layer. It is built in TCP
- **Checksums**
  - It ensures the integrity of data packets
- **Timers**
  - It indicates whether the packed is recieved on the other end timely.
- **Sequence Numbers**
  - Every data packet has a unique sequence numbers which prevents packet redundancy


#### UDP (User Datagram Protocol)

- Connectionless protocol
- Data may or may not be delivered
- Data may change mid-travel
- Data maybe in different order
- UDP does uses checksums, but doesn't do much about corrupted data
- UDP packet:
  - Source Port (2 bytes)
  - Destination Port (2 bytes)
  - Length of datagram (2 bytes)
  - Checksum (2 bytes)
  - Data (2^16 - 8) bytes {Total UDP packet size is 2^16 bytes}

- Use cases: DNS, Video Conference, Online Gaming
- ` sudo tcpdump -c 5` command to check the number of packets recieved by a device. The `-c` flag is used to specify the number of packets we want to recieve.


#### TCP (Transmission Control Protocol)

- Application layer sends a lot of raw data -> TCP segments this data by dividing it into chunks and adding headers. 
- It may also collect the data from the Network layer (Scenario of the receiving end), and aggregate these chunks and sends to Application Layer
- Congestion Control
- It maintains the order of data using sequence numbers.

**3-Way Handshake**

- Client sends a `connection request` to the Server. It carries a flag called `SYNC` and a sequence number which will be a random number in order to make guessing difficult
- Server sends an `ACK` (Acknowledgement) flag, `SYNC` flag and it sends a sequence number which is a result of some calculation applied on the sequence number from Client.
- Client sends the acknowledges the signal from the Server, and thus connection is established.

### Networking Layer

- Router to Router communication
- **Fowarding Table**: Usually the packet contains the destination network address. Once the packet is recieved by the router, it check in its forwarding table, and send the packet to appropriate router. It only contains one path defined
- Say, we have an IP address: `192.168.2.30`. Here `192.168.2` is the network address, and `30` is the device address which is connected to the said network

**Control Plane**

- There are used to build Routing tables.
- Think of graph where Routers are nodes, and the link between routers are edges.
- **Static Routing**
  - Adding addresses manually
  - Pretty time consuming
- **Dynamic Routing**
  - It changes according to changes in the network

#### Internet Protocol (IP)

- It used for logical Network addressing (IP addresses)
- There are two types of IP addresses: IPv4 and IPv6
- IPv4
  - 32 bits, 4 words
- IPv6
  - 128 bits

- Classes of IP addresses
  - Class A - `0.0.0.0` to `127.255.255.255`
  - Class B - `128.0.0.0` to `191.255.255.255`
  - Class C - `192.0.0.0` to `223.255.255.255`
  - Class D - `224.0.0.0` to `239.255.255.255`
  - Class E - `240.0.0.0` to `255.255.255.255`

#### Subnet Mask

A subnet mask is a number that defines the relationship between the network address and the host (device) address of a network. It is used to divide an IP address into two parts: the network portion and the host portion. The network portion identifies the network that the device is on, while the host portion identifies the specific device on that network.

The subnet mask is typically written in the same format as an IP address, using four numbers separated by periods. Each number can be a value from 0 to 255. For example, a common subnet mask is 255.255.255.0, which indicates that the first three octets (numbers) of the IP address represent the network portion, and the last octet represents the host portion.

Subnet masks are used to create subnetworks, or subnets, which are smaller networks within a larger network. Subnetting allows an organization to divide a large network into smaller, more manageable networks, and can be used to improve security, performance, and scalability.

For example, an organization with a large network might use subnetting to create separate subnets for different departments or locations, or to separate the network into segments for different types of devices or traffic. In this way, subnet masks allow organizations to better control and manage their network resources.

#### Packets in Network Layer