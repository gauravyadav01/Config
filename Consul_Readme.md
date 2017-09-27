# Condul Config

1. Download Consul Liniux 64 bit from https://www.consul.io/downloads.html
2. Create a directory layout 
    /opt/consul/{consul_version)/consul 
    
    eg: /opt/consul/0.9.3/consul 
3. Create a link 

   ln -s /opt/consul/0.9.3/consul  /usr/local/bin/consul 
   Make sure /usr/local/bin in $PATH.

4. Consul Config /etc/consul/consul.json.
   Please Change parameter accordign to your env.

```
{
  "bootstrap": true,
  "client_addr": "0.0.0.0",
  "datacenter": "wec",
  "data_dir": "/var/lib/consul",
  "ports": {
    "dns": 8600,
    "http": 8500,
    "serf_lan": 8301,
    "serf_wan": 8302,
    "server": 8300
  },
  "retry_join": [
    ""
  ],
  "server": true,
  "ui": true
}
```

5. Systemctl script

 /etc/systemd/system/consul.service

```
[Unit]
Description=consul
Wants=network.target
After=network.target

[Service]
Environment="GOMAXPROCS=2" "PATH=/usr/local/bin:/usr/bin:/bin"
ExecStart=/usr/local/bin/consul agent -config-file=/etc/consul/consul.json -config-dir=/etc/consul/conf.d
ExecReload=/bin/kill -HUP $MAINPID
KillSignal=TERM
User=consul
WorkingDirectory=/var/lib/consul

[Install]
WantedBy=multi-user.target
```

6. systemctl daemon-reload
   systemctl start consul


