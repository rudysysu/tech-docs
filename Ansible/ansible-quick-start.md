## example
```
ansible all -i k8s-1,k8s-2,k8s-3 -m command -a "sed -i 's/SELINUX=enforcing/SELINUX=permissive/g' /etc/selinux/config"
ansible k8s -m service -a 'name=firewalld state=stopped enabled=false'

```