# Dynamic Delegate And SOCKS 5

## Dynamic
Open a local port 1080, which connects to the remote HUB port 22.

- Session
	* Host Name: 147.128.64.133 // this is a HUB ip.
	* Port: 22
- Connection -> SSH -> Tunnnels
	* Type: Dynamic
	* Source port: 1080 // or any other port

## SOCKS 5
Use proxy to transfer all data to HUB.

- Session
	* Host Name: 10.175.193.13 // this is a LAB ip.
	* Port: 22
- Connection -> Proxy
	* Proxy type: SOCKS 5
	* Proxy hostname: 127.0.0.1
	* Port: 1080
- Connection -> SSH -> Tunnnels
	* Type: Local
	* Source port: 9092
	* Destination: 127.0.0.1:9092
	
## Reference
- https://www.chenyudong.com/archives/linux-ssh-port-dynamic-forward.html
