# Docker Fly

docker build repo for v2fly

https://hub.docker.com/r/implementsio/v2fly

## Usage

### Config

config_v5.json

```json
{
  "inbounds": [
    {
      "port": 1080,
      "protocol": "vmess",
      "settings": {
        "users": [
          "${UUID}"
        ]
      },
      "streamSettings": {
        "transport": "ws",
        "transportSettings": {
          "path": "/ws"
        }
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom"
    }
  ]
}
```

### Docker

```bash
docker run --rm implementsio/v2fly help

docker run --name v2ray implementsio/v2fly $v2ray_args (help, eun etc...)

docker run -d --name v2ray -v /path/to/config.json:/etc/v2ray/config.json -p 10086:10086 implementsio/v2fly run -c /etc/v2ray/config.json 

# If you want to use v5 format config
docker run -d --name v2ray -v /path/to/config.json:/etc/v2ray/config.json -p 10086:10086 implementsio/v2fly run -c /etc/v2ray/config.json -format jsonv5
```

### Docker Compose

docker-compose.yaml

```yaml
version: '3.6'
services:
  v2fly:
    image: implementsio/v2fly:v5.12.1
    restart: always    
    command: run -c /etc/v2ray/config.json -format jsonv5
    volumes:
      - ./config_v5.json:/etc/v2ray/config.json
    ports:
      - 1080
    networks:
      - v2fly

networks:
  v2fly:
    name: v2fly
    driver: bridge
```

start docker containers

```bash
docker-compose up -d
```
