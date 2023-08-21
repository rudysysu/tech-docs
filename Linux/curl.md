## Example
- curl -LO http://host:port/xxx/xxxx  
  -L: 表示当遇到 HTTP 响应中的重定向时，curl 将自动跟随重定向。换句话说，它告诉 curl 在遇到 HTTP 3xx 响应状态码时自动重定向到新的 URL 地址。  
  -O: --remote-name, Write output to a local file named like the remote file we get.
