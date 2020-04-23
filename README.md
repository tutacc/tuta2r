# tuta2r
A stand-in of udp2raw

## Usage

Run udp2raw-tunnel on docker compose

client:
```yaml
 # server docker-compose.yml

 version: '3'
 services:
   udpspeeder:
     image: tutacc/tuta2r
     restart: unless-stopped
     command: -s -l 0.0.0.0:4001 -r 127.0.0.1:4000 -k pass --raw-mode faketcp -a
     cap_add:
       - NET_ADMIN
     network_mode: "host"
 # client docker-compose.yml
```

server:
```yaml
 version: '3'
 services:
   udp2raw:
     image: tutacc/tuta2r
     restart: unless-stopped
     command: -c -r ${SERVER_ADDR}:4001 -l 127.0.0.1:4000 --raw-mode faketcp -a -k pass
     cap_add:
       - NET_ADMIN
     network_mode: "host"
```
