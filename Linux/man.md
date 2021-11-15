## man

### 解决 No manual entry for X 问题
https://github.com/tianon/docker-brew-ubuntu-core/issues/122
```
rm /etc/dpkg/dpkg.cfg.d/excludes

apt-get update && \
dpkg -l | grep ^ii | cut -d' ' -f3 | xargs apt-get install -y --reinstall && \
rm -r /var/lib/apt/lists/*
```