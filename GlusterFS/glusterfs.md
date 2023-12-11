
## Install
ansible k8s -m yum -a 'name=centos-release-gluster state=present disablerepo=kubernetes'  
ansible k8s -m yum -a 'name=glusterfs-server state=present disablerepo=kubernetes'  
ansible k8s -m service -a 'name=glusterd state=started enabled=yes'  

ansible k8s-1 -m yum -a 'name=heketi state=present disablerepo=kubernetes'  
ansible k8s-1 -m yum -a 'name=heketi-client state=present disablerepo=kubernetes'  

## Config Heketi
k8s-1:  
	ssh-keygen   
	ssh-copy-id root@k8s-1  
	ssh-copy-id root@k8s-2  
	ssh-copy-id root@k8s-3  
	cp .ssh/id_rsa /etc/heketi/glusterfs_key  
	cp assets/heketi.json /etc/heketi/heketi.json  
	systemctl enable heketi.service  

ansible k8s-1 -m lineinfile -a 'dest=/usr/lib/systemd/system/heketi.service regexp="^User=" line=User=root'  

## Topology Setup
heketi-cli topology load --json=topology.json  

## Command
heketi-cli topology load --json=topology.json  
heketi-cli cluster list  
heketi-cli cluster info d80bd062da5eff0450f527d431f110c4
heketi-cli node info 6715f4f566da1840cbc968c0acb9bc72
heketi-cli device info eb3130bf34855f23d1120357a65c1656


## References
- https://docs.gluster.org/en/latest/
- https://wiki.centos.org/SpecialInterestGroup/Storage/gluster-Quickstart
- https://blog.csdn.net/phn_csdn/article/details/75153913?utm_source=debugrun&utm_medium=referral