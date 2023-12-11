deprecated, please refer to security part

### Specify the certification user
```bash
vi /etc/sslopenssl.cnf

[ v3_req ]
subjectAltName = @alt_names

[ alt_names ]
DNS.1 = *.rudysysu.com
```

### Build unsecure key for nginx
```bash
openssl rsa -in rudysysu.pem -out rudysysu.pem.unsecure
```

## Delete Certification
```cmd
certmgr.msc
```
