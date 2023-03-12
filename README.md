## IPv6 Proxy Server [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Create your own IPv6 backconnect proxy server with only one script on any Linux distribution. Any number of random IPs on the subnet, ideal for parsing and traffic arbitrage (Google/Facebook/Youtube/Instagram and many others support IPv6).

Ask questions: [@just_temp](https://t.me/just_temp)

### Tutorial

Assuming you already have an entire IPv6 subnet (/48 or /64) routed to your server.

Just run:

```bash
#sudo su
git clone https://github.com/Theodikes/ipv6-proxy-server.git && cd ipv6-proxy-server
chmod +x ipv6proxyserver-install.sh
./ipv6proxyserver-install.sh -s 64 -c 100 -u username -p password -t http -r 10
```

Uncomment first line or run all commands with `sudo` if you`re not under root.

**Command line arguments:**

- `-s` or `--subnet` - IPv6 [subnet](https://docs.netgate.com/pfsense/en/latest/network/ipv6/subnets.html), fully dedicated for your server. `48` or `64`, default `64`
- `-c` or `--proxy-count` - The total number of proxies you want to have (from 1 to 10000)
- `-t` or `--proxies-type` - Proxies type - `http` or `socks5`. Default `http`, if no value provided
- `-u` or `--username` - All proxies auth login (required)
- `-p` or `--password` - All proxies auth password (required)
- `--start-port` - backconnect IPv4 start port. If you create 1500 proxies and `start-port` is `20000`, and server external IPv4 is, e.g,`180.113.14.28` you can connect to proxies using `180.113.14.28:20000`, `180.113.14.28:20001` and so on until `180.113.14.28:21500`
- `-r` or `--rotating-interval` - rotation interval of entire proxy pool in minutes. At the end of each interval, output (external IPv6) addresses of all proxies are changed and proxy server is restarted, which breaks existing connections for a few seconds. From 0 to 59, default value - `0` (rotating disabled)
- `-l` or `--localhost` - bool parameter without value, if used, all backconnect proxy will be available only on localhost (`127.0.0.1:30000` instead of `180.113.14.28:30000`)
- `-m` or `--ipv6-mask` - first blocks on server subnet, unchanged part, use ONLY if script cannot parse ipv6 mask automatically. For example, if the external ipv6 address on server is `2a03:6f01:5::1da6` and you want to use entire /64 subnet, script cannot parse ipv6 gateaway because of address zero-field replacement with `::`. Real mask for /64 subnet is first four blocks - `2a03:6f01:5:0`

### License

[MIT](https://opensource.org/licenses/MIT)