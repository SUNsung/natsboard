# NATSboard

[![NPM][npm-image]][npm-url] [![Build Status][travis-image]][travis-url]

Dashboard for monitoring NATS. It provides real-time information from NATS server. 

![Overview](public/img/ss-natsboard-v3-1.png)

![Connections](public/img/ss-natsboard-v3-2.png)

![Routes](public/img/ss-natsboard-v3-4.png)

![Dashboard](public/img/ss-natsboard-v3-3.png)

## Installation

```bash
npm install natsboard -g
```

## Usage

[gnatsd server](http://nats.io/download/) **must** be running with `-m` parameter.

```bash
gnatsd -m 8222
natsboard

# Custom port
gnatsd -m 12345
natsboard --nats-mon-url http://localhost:12345
```

## Usage by linux-service
```bash
useradd -r -c 'NATS monitoring' nats_monitor
nano /etc/systemd/system/nats-monitoring.service
```
in file: (path to natsboard: **which natsboard**)
```
[Unit]
Description=NATS monitorig server
After=syslog.target network.target

[Service]
Type=simple
ExecStart=/{FULL PATH}/natsboard --nats-mon-url http://{YOUR HOST}:{YOUR PORT}
User=nats_monitor
Group=nats_monitor
LimitNOFILE=65536
ExecReload=/bin/kill -HUP $MAINPID
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

Start service:
```bash
systemctl enable nats-monitoring --now
```
Status service:
```bash
systemctl status nats-monitoring
```

## License

Licensed under The MIT License (MIT)  
For the full copyright and license information, please view the LICENSE.txt file.

[npm-url]: http://npmjs.org/package/natsboard
[npm-image]: https://badge.fury.io/js/natsboard.svg

[travis-url]: https://travis-ci.org/devfacet/natsboard
[travis-image]: https://travis-ci.org/devfacet/natsboard.svg?branch=master
