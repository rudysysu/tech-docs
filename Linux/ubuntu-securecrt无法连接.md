## 使用SecureCRT连接Ubuntu20.04报错：Key exchange failed. No compatible key exchange method.
新安装的Ubuntu20.04，SSH服务已安装，使用putty可以正常ssh远程登录进去，使用SecureCRT远程登录会报错如下：Key exchange failed. No compatible key exchange method. The server supports these methods: curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group14-sha256

在/etc/ssh/sshd_config文件中添加
```
KexAlgorithms curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1,diffie-hellman-group-exchange-sha1,diffie-hellman-group1-sha1
```

`$sudo /etc/init.d/ssh restart`
