# install-kcp

### Standard Install

Install kcp `v0.11.0` to /etc/kcp and enable/start the service on port 6443:

`ansible-playbook install-kcp.yaml`
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
_the kcp service is managed using systemd:_

`sudo systemctl (start/stop/restart) kcp`

##### Logs:
`journalctl -eu kcp`
##### Live logs:
`journalctl -eu kcp -f`


### Custom Install

Override variables in `install-kcp.yaml` or pass them as extra_vars on the command line with `-e`:

`ansible-playbook install-kcp.yaml -e "kcp_extra_args=--feature-gates=KCPSyncerTunnel=true"`
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
             └─80380 /usr/local/bin/kcp start --feature-gates=KCPSyncerTunnel=true
```

### Install using Binaries Built from Source

Use `-e build=true` to install kcp using binaries built from source (kcp-dev/kcp:main):

`ansible-playbook install-kcp.yaml -e build=true`

Build from alternate branches and forks by passing the `source_repo` and `source_branch` extra_vars:

`ansible-playbook install-kcp.yaml -e build=true -e source_repo=aknochow/kcp -e source_branch=main`
