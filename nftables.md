# Nftables Hands On

## Task Requirements

Using `nftables` (`iptables` is also acceptable), implement rules to transparently redirect specific TCP and UDP connections. Your goal is to redirect traffic destined for a public address-port combination (e.g. `1.2.3.4:443`) to a local service running on `127.0.0.1`.

- **TCP Redirection**: Redirect incoming TCP packets destined for `1.2.3.4:443` to `127.0.0.1:10443`.

- **UDP Redirection**: Redirect incoming UDP packets destined for `1.2.3.4:53` to `127.0.0.1:10053`.

- **Entire IP Redirection**: Redirect all traffic destined for `2.3.4.5` to `127.0.0.2`.

## Local Testing
To verify your rules are working correctly, you can use a tool like `netcat` or `socat` to listen for connections on the local ports.

```sh
socat TCP4-LISTEN:10443,fork,reuseaddr TCP4:example.com:443 &
socat UDP4-LISTEN:10053,fork,reuseaddr UDP4:8.8.8.8:53 &
python3 -m http.server 8000 --bind 127.0.0.2 &
```


- TCP: Test your TCP redirection rule using `curl`. The connection should be received by your local listener on port 10443.

```sh
curl https://example.com --resolve example.com:443:1.2.3.4 -v
```

- UDP: Test your UDP redirection rule using dig. The DNS query should be received by your local listener on port 10053.

```sh
dig @1.2.3.4 example.com
```

- IP: Test your IP redirection rule by pinging the redirected IP address.

```sh
ping 2.3.4.5
```

## Hints

You may use `tcpdump` to observe the traffic and verify that your redirection rules are functioning as expected.

## Deadline
Tentatively due before Monday of the second week.

## Reference Material

- [Nftables Wiki](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page)
- Man pages: nft(8), iptables(8)