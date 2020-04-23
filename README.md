# tuta2r
A stand-in of udp2raw

## Usage

Run udp2raw-tunnel on docker compose

server:
```yaml
version: '3'
services:
  tuta2r:
    image: tutacc/tuta2r
    restart: unless-stopped
    command: -s -l 0.0.0.0:4001 -r 127.0.0.1:4000 -k pass --raw-mode faketcp -a
    cap_add:
      - NET_ADMIN
    network_mode: "host"
```
其中4000为你的服务端口，4001为tuta2r(udp2raw)开放的端口。

client:
```yaml
version: '3'
services:
  tuta2r:
    image: tutacc/tuta2r
    restart: unless-stopped
    command: -c -r ${SERVER_ADDR}:4001 -l 127.0.0.1:4000 --raw-mode faketcp -a -k pass
    cap_add:
      - NET_ADMIN
    network_mode: "host"
```
其中4001为你的服务器tuta2r(udp2raw)开放的端口，4000为服务端口。
