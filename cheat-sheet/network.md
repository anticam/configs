# Tools
### sslscan
```shell
❯ sslscan --show-sigs --show-client-cas --show-certificate google.com
Version: 2.1.1 Windows 64-bit (Mingw)
OpenSSL 3.0.9 30 May 2023

Connected to 2a00:1450:4001:830::200e

Testing SSL server google.com on port 443 using SNI name google.com

  SSL/TLS Protocols:
SSLv2     disabled
SSLv3     disabled
TLSv1.0   enabled
TLSv1.1   enabled
TLSv1.2   enabled
TLSv1.3   enabled
```

### nslookup
look for IP address with local DNS
```shell
nslookup telekom.hu
```

look for IP address using a Google DNS
```shell
nslookup telekom.hu 8.8.8.8
nslookup telekom.hu 8.8.4.4
```
look for IP address using Cloudflare DNS
```shell
nslookup telekom.hu 1.1.1.1
```

### Fast.com
Speedtest from browser [fast.com](https://fast.com)  
Speedtest from CLI - [Test Your Internet Speed from the Linux Terminal with fast](https://technotim.live/posts/fast-internet-test-cli/)  
