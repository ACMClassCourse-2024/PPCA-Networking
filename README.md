# PPCA Networking Project

## Project Introduction

Understand the basic components of computer networks, learn about relevant protocols, and equip yourself with a handful of tools you'll use in your daily life.

## Important Notes

* PPCA is not a project designed for intense competition. As long as you follow the basic rules and complete the necessary tasks, you don't need to worry about your grade at all.
* Therefore, we hope that everyone chooses a project they are genuinely interested in, rather than just doing it for the grade.
* We hope everyone has fun.

## Project Requirements

The basic tasks are required to be completed in the first week. In the following three weeks, you need to complete at least 4 intermediate or advanced tasks, with at least one task chosen from the advanced categories.

We hope that the tools you implement will be something you will truly use in your later life, weathering the test of real-world usage. Usability, code quality and commit hygiene will be considered in code review.

### Basic (25%)

- [Simple SOCKS5 Proxy Server](socks5.md)

- [Nftable Basics](nftables.md)

### Intermediate (15% each)

#### 1. Transparent proxy based on `nftables` and `tproxy`
  Using an existing virtual tun implementation is also acceptable, so long as you write the `nftables` rules yourself.

#### 2. Socks5 server with UDP support
  UDP NAT behavior is limited to Full Cone or Symmetric.

  You may find most `socks5` client implementations out there do not obey RFC in terms of UDP behavior, or do not support UDP at all. The writer ultimately found one that does, but has forgotten the name.

#### 3. TLS Hijacking
  Capture and inspect HTTPS traffic just like `mitmproxy` does.

#### 4. Customized DNS Server and SNI Proxy
  Although you may write a standalone demo first, you should implement these two features on a popular networking tool with high code quality.

#### Anything else

### Advanced (25% each, w/ ranking based scoring)

**Note:** Task 2 is composed of two parts (2.1 and 2.2). Both parts must be completed to be considered one full advanced task. Completing only one part will be counted as 0.5 advanced tasks.

#### 1. Simple `frp`
  A simple implementation of `frp` (Fast Reverse Proxy) that maps a port on a local machine `A` in the intranet to a port on a remote machine `B` in the internet, allowing the internet to access the service on `A` through `B`.

  The implementation should support both TCP and UDP protocols, and support both TCP and QUIC in the transport layer.

  Security should be enforced with mutual TLS authentication, with utilities to generate certificates and keys for both `A` and `B` based on `openssl`.

  Bandwidth and latency should be comparable to the original `frp` implementation under 1Gbps network conditions.

  Also, your implementation should be different from the original `frp` implementation.

#### 2. Advanced `nftables` tasks

##### 2.1 Transparent proxy on a secondary gateway
  Most tutorials on the internet only show how to set up a transparent proxy on the primary gateway, i.e., the router.

  However, if the primary gateway crashes, the entire network will be affected.

  Therefore, it is a better idea to set up the transparent proxy on a secondary device in the network, such as an old Linux laptop or a Raspberry Pi.

  Other devices in the network can be transparently proxyed by simply setting the secondary device as the gateway, without installing any software on them.

##### 2.2 Ghost IP: Make a Remote Server Appear on Your Network via WireGuard and NDP Proxy
  Suppose you have a server `A` outside your LAN, and a server `B` inside your LAN. You need to make `A` appear as if it is on the same network as `B`, so that devices in your LAN can access `A` using its local IP address. Further requirements:
  - `A` should have independent IPv4 and IPv6 addresses, different from `B`.
  - `A` should be able to access devices in `B`'s network, including those outside `B`'s assigned IP-CIDR, and vice versa.
  - The outgoing traffic from `A` should **not** go through `B`, but directly to the internet.
  - Devices in `A`'s original network should still be able to access `A` using its original IP address.

#### 3. Virtual TUN device for IKEv2 VPN
  Implement a virtual TUN device that acts as a VPN client for IKEv2. But instead of routing all traffic through the VPN, like a standard VPN client, it exposes the virtual network as a SOCKS5 proxy server.

  This allows for more flexible routing of traffic through the VPN, as you can choose which applications use the VPN, or which domains are routed through the VPN.

  You can either implement a standalone binary, or integrate it into a popular networking tool with high code quality.

#### 4. Custom SNI Proxy for HTTP/3
  Implement a non-standard SNI proxy that can handle HTTP/3 traffic with custom clients.

#### Anything else
If there are any other features you want to implement yourself, you can apply to the TA. After the TA evaluates the workload, an appropriate point value will be assigned.

## Grading Criteria

  * **Basic Task:** 25%
  * **Intermediate Task:** 15% each
  * **Advanced Task:** 25% each, w/ ranking based scoring
  * **Bonus:** 10%

Notes:
  * **Do not** expect to get a full score easily in the intermediate and advanced tasks. Usability, code quality and commit hygiene will be considered in code review.
  * We hope that everyone try out different realms of networking. If multiple people choose the same **advanced** task, **only the best implementation will receive full points**.

## Reference Materials

**Reference Books:**

  * [Beej’s Guide to Network Programming](https://beej.us/guide/bgnet/)
  * [High Performance Browser Networking](https://hpbn.co/)
      * The content of this book goes far beyond the requirements of this project. You only need to read the "Networking 101" section and parts of the "HTTP" section.
  * [TCP/IP Tutorial and Technical Overview](https://www.redbooks.ibm.com/redbooks/pdfs/gg243376.pdf)

**Protocol Documents:**

  * [RFC 1928: SOCKS Protocol Version 5](https://www.rfc-editor.org/rfc/rfc1928)
  * [RFC 1035: Domain Names - Implementation and Specification](https://www.rfc-editor.org/rfc/rfc1035)
  * [RFC 9293: Transmission Control Protocol (TCP)](https://www.rfc-editor.org/rfc/rfc9293)
  * [RFC 768: User Datagram Protocol](https://www.rfc-editor.org/rfc/rfc768)
  * [RFC 1149: A Standard for the Transmission of IP Datagrams on Avian Carriers](https://www.rfc-editor.org/rfc/rfc1149)
  * [RFC 9112: HTTP/1.1](https://www.rfc-editor.org/rfc/rfc9112.html)
  * [RFC 9114: HTTP/3](https://www.rfc-editor.org/rfc/rfc9114.html)
  * [HTTP on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP)
  * [RFC 8446: The Transport Layer Security (TLS) Protocol Version 1.3](https://www.rfc-editor.org/rfc/rfc8446)

**Blogs and Articles:**

  * Cloudflare Blogs, such as [tls handshake](https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/), [tls 1.3](https://blog.cloudflare.com/rfc-8446-aka-tls-1-3/), (recommended by Hanning Wang)
  * Wikipedia Articles, such as [SOCKS5](https://en.wikipedia.org/wiki/SOCKS)


Feel free to add more.

## Acknowledgments

Thanks to Alan Liang from the 2021 ACM Class for laying the foundation for this project.