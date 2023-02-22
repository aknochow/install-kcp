# install-kcp

### Standard Install

`ansible-playbook install-kcp.yaml`

This will install kcp `v0.10.0` on port 6443 and enable/start the service:
```
systemctl status kcp
● kcp.service - kcp
     Loaded: loaded (/etc/systemd/system/kcp.service; enabled; preset: disabled)
     Active: active (running) since Wed 2023-02-22 12:47:06 EST; 5s ago
       Docs: https://docs.kcp.io
   Main PID: 80962 (kcp)
      Tasks: 11 (limit: 9440)
     Memory: 206.6M
        CPU: 4.105s
     CGroup: /system.slice/kcp.service
             └─80962 /usr/local/bin/kcp start --secure-port 6443
```

### Custom Install

You can override variables in the install-kcp.yaml or pass them on the command line.

`ansible-playbook install-kcp.yaml -e "kcp_secure_port=6447" -e "kcp_extra_args=--feature-gates=KCPSyncerTunnel=true"`
```
systemctl status kcp
● kcp.service - kcp
     Loaded: loaded (/etc/systemd/system/kcp.service; enabled; preset: disabled)
     Active: active (running) since Wed 2023-02-22 12:45:20 EST; 11s ago
       Docs: https://docs.kcp.io
   Main PID: 80380 (kcp)
      Tasks: 12 (limit: 9440)
     Memory: 211.5M
        CPU: 4.520s
     CGroup: /system.slice/kcp.service
             └─80380 /usr/local/bin/kcp start --secure-port 6447 --feature-gates=KCPSyncerTunnel=true
```

Install a specific version of kcp:

`ansible-playbook install-kcp.yaml -e "kcp_version=0.11.0"`
```
kcp --version
kcp version v1.24.3+kcp-v0.11.0
```
