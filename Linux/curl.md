# Curl

## Command
~~~shell
curl http://ip:port/xxx
~~~

## Options
```shell
-X, --request <command>: Specifies a custom request method GET, HEAD, POST and PUT 
--basic: Tells curl to use HTTP Basic authentication.
--digest: Enables HTTP Digest authentication.
-u, --user <user:password> <user:password>: Specify the user name and password to use for server authentication.
-H, --header <header>: Extra header to use when getting a web page.
-d, --data <data>: Sends the specified data in a POST request to the HTTP server
-o, --output <file>: Write  output to <file> instead of stdout.
-O, --remote-name: Write  output  to a local file named like the remote file we get.
-v, --verbose:  Makes  the fetching more verbose/talkative.
-L: (HTTP) If the server reports that the requested page has moved to a different location (indicated with a Location: header and a 3XX response code), this option will make curl redo the request on the new place.
-x, --proxy [PROTOCOL://]HOST[:PORT] Use proxy on given port
-i, --include       Include protocol headers in the output (H/F)
-I, --head          Show document info only
```

## Example
```shell
-X POST 
--header "Content-Type:application/json" --header "Accept:application/json" --header "Content-Type:application/json"
-u trip-user:pswFMS179!
--basic --user trip-user:pswFMS179!
-d '{}'
-d @filename
```

```
- curl -LO http://host:port/xxx/xxxx  
  - -L: 表示当遇到 HTTP 响应中的重定向时，curl 将自动跟随重定向。换句话说，它告诉 curl 在遇到 HTTP 3xx 响应状态码时自动重定向到新的 URL 地址。  
  - -O: --remote-name, Write output to a local file named like the remote file we get.
```
