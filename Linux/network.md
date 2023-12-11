# Network

## Delegate
- Available environment variables are
  - http_proxy
  - https_proxy
  - ftp_proxy
  - socks_proxy
  - all_proxy
  - no_proxy
- Example
```
vi /etc/profile
export all_proxy=http://www-proxy.lmera.ericsson.se:8080
```
- Apply
```
source /etc/profile
. /etc/profile
source /etc/environment
. /etc/environment
OR just logout and login again.
```
- Reference
  - https://www.linuxsecrets.com/entry/6-managing-linux-systems/2015/05/26/1490-manually-change-ubuntu-proxy-settings-from-cli-command-line-terminal
