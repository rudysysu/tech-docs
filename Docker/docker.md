#### 修改images本地目录
mklink /J C:\Users\Rudy\AppData\Local\Docker\wsl\data D:\data\docker

## Installation
- https://docs.docker.com/engine/install/ubuntu/

## Start/Stop Docker
- systemctl start/stop/status docker
- service docker start

## Test Docker
- docker run hello-world

## 开启2375端口
```
# vim /usr/lib/systemd/system/docker.service
[Service]
# ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock -H tcp://0.0.0.0:2375

# systemctl daemon-reload
# systemctl restart docker

# curl http://localhost:2375/version
```
