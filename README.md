# pathfinder
WebSocket-over-Kafka reverse proxy

# Usage
```
USAGE:
    pathfinder [OPTIONS]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -c, --config <config>            Path to a custom settings file [default: ""]
    -i, --ip <ip>                    The used IP for a server [default: 127.0.0.1]
    -x, --kafka-ip <kafka_ip>        The used IP by Kafka broker [default: 127.0.0.1]
    -z, --kafka-port <kafka_port>    The listened port by Kafka broker [default: 9092]
    -p, --port <port>                The listened port by Kafka broker [default: 8080]
    -C, --cert <ssl_certificate>     Path to a SSL certificate [default: ""]
    -K, --key <ssl_public_key>       Path to a SSL public key [default: ""]
```

# Configuration file  
For using a custom configuration for reverse proxy, you will need to specify `-c` (or `--config`) option with a path to 
a file. For example:
```bash
pathfinder --config=myconfig.yaml -p 8001
```
At the current stage of this project, reverse proxy is support only endpoints list, which is using for mapping URLs into certain Kafka topics. 
Each of those endpoints contains two fields: 
- `url` - URL that specified by a client in each request. 
- `microservice` - Means the name of topic (or queue) where will be storing the message. This topic (or queue) is listening by certain microservice.

### Example
```yaml
endpoints:
  - search:
     url: "/api/matchmaking/search"
     microservice: "microservice.search"
  - leaderboard:
     url: "/api/matchmaking/leaderboard"
     microservice: "microservice.leaderboard"
```

# Documentation
Information about why this reverse proxy was implemented you can find [here](https://github.com/OpenMatchmaking/documentation/blob/master/docs/components.md#reverse-proxy).

# License
The pathfinder is published under BSD license. For more details read the [LICENSE](https://github.com/OpenMatchmaking/pathfinder/blob/master/LICENSE) file.
