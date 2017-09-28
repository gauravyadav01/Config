Systemd nomad.service
```
[Unit]
Description = Nomad System Scheduler

[Service]
ExecStart = /usr/local/bin/nomad agent -config=/etc/nomad-conf.d
Restart = on-failure

[Install]
WantedBy = multi-user.target
```

Server: /etc/nomad.d/config.json

```
{
	"data_dir": "/var/lib/nomad",
	"bind_addr": "IP_ADDR",
	"region": "us-wec",
	"datacenter": "wec",
	"client": {
		"enabled": false
	},
	"server": {
		"enabled": true,
		"bootstrap_expect": 2
	}
}
```
Client /etc/nomad.d/config.json

```
{
	"data_dir": "/var/lib/nomad",
	"bind_addr": "IP_ADDR",
	"datacenter": "wec",
	"region": "us-wec",
	"client": {
		"enabled": true
	},
	"server": {
		"enabled": false,
		"bootstrap_expect": 2
	}
}
```

