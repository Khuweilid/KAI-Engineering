# Networking Foundation

## Why I am learning networking

I need networking because intelligent systems do not operate as isolated programs.

Sensors, computers, servers, gateways, cloud systems and services need to communicate.

My basic networking mental model is:

Application → Socket → TCP/UDP → Port → IP → Routing → Gateway → Network interface → Link

## 1. Network interfaces

I learned that Linux uses network interfaces to connect the operating system to networks.

I used:

```bash
ip link
ip addr
```

to inspect interfaces and addresses.

The loopback interface is used for communication within the local machine.

## 2. IPv4

IPv4 uses 32 bits and is normally written as four decimal octets.

Example:

```text
192.168.100.41
```

An IPv4 address works together with a prefix such as `/24` to define the local network and host portion.

## 3. Private IPv4 ranges

The main private ranges I learned are:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

Private addresses are commonly used inside local networks.

## 4. CIDR

CIDR notation tells me how many bits belong to the network portion.

For example:

```text
192.168.100.41/24
```

means 24 network bits and 8 host bits.

The subnet mask is:

```text
255.255.255.0
```

I also worked through an older `/20` example from my WSL environment:

```text
172.18.169.158/20
```

which belongs to:

```text
172.18.160.0/20
```

That example is historical because my current system is native Ubuntu.

## 5. Gateway and routing

A default gateway is normally used when a destination is outside the local network.

I used:

```bash
ip route
```

and:

```bash
ip route get 8.8.8.8
```

to understand how Linux decides where to send traffic.

## 6. DNS

DNS converts names such as:

```text
google.com
```

into IP addresses that systems can use for communication.

I used:

```bash
getent hosts google.com
```

and examined the resolver configuration.

## 7. TCP and UDP

I learned the basic difference between TCP and UDP and how they operate above IP.

TCP provides a connection-oriented transport mechanism.

UDP provides a connectionless transport mechanism.

The important point for me is that IP alone does not identify the application that should receive traffic.

## 8. Ports and sockets

A port identifies an application/service endpoint on a host.

A socket can be understood as a communication endpoint involving an address and port.

My mental model is:

Application → Socket → TCP/UDP → Port → IP

## 9. Inspecting sockets

I used:

```bash
ss -tuln
```

to see listening TCP and UDP sockets.

This connected the networking concepts to actual services running on Linux.

## 10. Network troubleshooting

I started using a layered approach.

If something does not work, I should not immediately assume the application is broken.

I can check:

1. Interface
2. IP address
3. Local network
4. Gateway
5. Routing
6. External IP connectivity
7. DNS
8. TCP port/service
9. Application protocol

## Current native Ubuntu network

My current native Ubuntu baseline is:

```text
Interface:       wlp0s20f3
Wi-Fi:           Kleen
IPv4:            192.168.100.41/24
Network:         192.168.100.0/24
Gateway:         192.168.100.1
DNS:             192.168.100.1
```

The current network is working.

## What I have learned

Networking is not just about IP addresses.

It is a chain:

Application → Transport → IP → Routing → Interface → Network → Destination

Understanding each layer will help me troubleshoot and later design real systems.

## Status

Networking foundations and the native Ubuntu baseline are completed.

Next: IPv4 binary and subnetting.
