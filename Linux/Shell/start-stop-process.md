# Start Stop Process

## start.sh
```bash
#!/bin/bash

ps aux | grep java | grep app.jar
if [ $? -ne 0 ]
then
  sudo su -c 'nohup /usr/local/app/lib/app.jar 2>&1 &' - app
fi
```

## stop.sh
```bash
#!/bin/bash

ps aux | grep java | grep app.jar
if [ $? -eq 0 ]
then
  sudo su -c 'ps axu | grep java | grep app.jar | awk '{print $2}' | xargs kill' - app
fi
```