# Native Ubuntu Networking Baseline

## Objective

I wanted to establish a fresh networking baseline on my current native Ubuntu workstation.

The old networking experiments were done in WSL, so I wanted current evidence from the native Ubuntu system.

## System identity

I ran:

```bash
hostname
```

Result:

```text
KAI-Workstation
```

## Network interfaces

I ran:

```bash
nmcli device status
```

The active network interface was:

```text
wlp0s20f3
```

The Wi-Fi connection was:

```text
Kleen
```

The loopback interface was also available.

## IPv4 configuration

I ran:

```bash
ip -4 addr
```

My active IPv4 configuration was:

```text
192.168.100.41/24
```

The broadcast address shown was:

```text
192.168.100.255
```

This means my current local network is:

```text
192.168.100.0/24
```

## Routing table

I ran:

```bash
ip route
```

The default route was:

```text
default via 192.168.100.1 dev wlp0s20f3
```

The local network route was:

```text
192.168.100.0/24 dev wlp0s20f3
```

This showed me that traffic for destinations outside the local subnet is sent through:

```text
192.168.100.1
```

## Route to an external address

I ran:

```bash
ip route get 8.8.8.8
```

Linux returned a route using:

```text
gateway: 192.168.100.1
interface: wlp0s20f3
source: 192.168.100.41
```

This confirmed how Linux would send traffic toward that destination.

## DNS

I ran:

```bash
resolvectl status
```

The current DNS server was:

```text
192.168.100.1
```

The interface was marked as having the default DNS route.

## Listening sockets

I ran:

```bash
ss -tuln
```

I saw local DNS listeners on:

```text
127.0.0.53:53
127.0.0.54:53
```

I also saw other local UDP/TCP listeners.

This helped me connect the idea of ports and sockets to actual services on my machine.

## Connectivity test 1 — loopback

I ran:

```bash
ping -c 4 127.0.0.1
```

Result:

```text
4 packets transmitted
4 received
0% packet loss
```

This confirmed local loopback connectivity.

## Connectivity test 2 — external IPv4

I ran:

```bash
ping -c 4 8.8.8.8
```

Result:

```text
4 packets transmitted
4 received
0% packet loss
```

The average response time was about:

```text
15.5 ms
```

This confirmed external IPv4 connectivity.

## Connectivity test 3 — DNS

I ran:

```bash
getent hosts google.com
```

The command returned an IPv6 address for Google.

This showed that name resolution was working.

## Connectivity test 4 — HTTPS

I ran:

```bash
curl -I https://google.com
```

The server returned:

```text
HTTP/2 301
```

with a redirect to:

```text
https://www.google.com/
```

This confirmed that the system could complete an HTTPS request.

## My troubleshooting chain

The tests gave me this:

```text
Local IP stack
      ↓
External IPv4
      ↓
DNS resolution
      ↓
HTTPS application request
```

All of these tests succeeded.

## What I learned

My native Ubuntu network is working and I now have current evidence of:

- active interface
- IPv4 address
- subnet
- default gateway
- routing
- DNS
- sockets
- external connectivity
- HTTPS connectivity

## Important note about the old WSL data

The previous WSL address was:

```text
172.18.169.158/20
```

That was useful for learning but it is not my current native Ubuntu address.

My current native Ubuntu address is:

```text
192.168.100.41/24
```

I should keep those two environments separate in my documentation.

## Engineering connection

This baseline gives me a real starting point for learning subnetting and later troubleshooting networks on Linux.

## Status

Completed.
