## Start
```bash
# elasticsearch
ps aux | grep java | grep elasticsearch
if [ $? -ne 0 ]
then
  sudo su -c 'cd /usr/local/elasticsearch && bin/elasticsearch -d' - elasticsearch
fi
```

## Stop
