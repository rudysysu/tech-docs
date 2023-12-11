#!/bin/bash

# define several variables for service control.
COMPONENT_HOME=$(cd "$(dirname "$0")/../"; pwd)
CORE_USER=ecf_core
COMPONENT_NAME="trip-mgmt"
JAR_FILE=${COMPONENT_HOME}/lib/trip-service-1.0-SNAPSHOT.jar
LOG_CONFIG_FILE=${COMPONENT_HOME}/conf/logback.xml
LOG_PATH=/var/log/ecf/vehicle-mobility/trip-mgmt

if [ ! -f ${LOG_CONFIG_FILE} ];then
  LOG_CONFIG_FILE=${COMPONENT_HOME}/conf/log4j2.xml
fi

#load environment variables from script if it exists.
if [ -f ${COMPONENT_HOME}/bin/env.sh ];then
  . ${COMPONENT_HOME}/bin/env.sh
fi

if [ -z ${JAVA_HOME} ] && [ -f "/usr/bin/java" ];then
  JAVA_EXEC="nohup /usr/bin/java"
else
  JAVA_EXEC="nohup ${JAVA_HOME}/bin/java"
fi

if [ -z "${JVM_ARGS}" ];then
  JVM_ARGS="-Xmx1G -Xms1G"
fi

if [ ! -f ${JAR_FILE} ];then
   echo "Couldn't find any jar files in specified path!"
   exit 1
fi

if [ `whoami` != ${CORE_USER} ];then
   JAVA_EXEC="sudo -u ${CORE_USER} ${JAVA_EXEC}"
fi

GRAPHITE_ARGS="-Dgroup=ECF-DEV -Dapp=TRIP-MGMT -Dinstance=trip-mgmt-1 -DgraphiteIp=192.168.1.23"

# define service control functions.
status(){
	COUNT=`ps --no-heading -C java -f --width 1000 |grep 'proc_name='${COMPONENT_NAME} | awk '{print $2}' | wc -l`
	if [ $COUNT -lt 1 ];then
		echo "Service "${COMPONENT_NAME}" is not running."
		exit 1
	else
		PIDS=`ps --no-heading -C java -f --width 1000 |grep 'proc_name='${COMPONENT_NAME} | awk '{print $2}'`
		echo "Service "${COMPONENT_NAME}" is running.Pid: "$PIDS
		exit 0
	fi
}

start(){
	COUNT=`ps -ef|grep 'proc_name='${COMPONENT_NAME} |grep -v grep|awk '{print $2}'|wc -l`
	if [ $COUNT -gt 0 ];then
		echo "INFO: The service "${COMPONENT_NAME}" is running!"
		exit 0
	fi
	# change directory to component's home.
	cd ${COMPONENT_HOME}

	${JAVA_EXEC} -server -Dproc_name=${COMPONENT_NAME} ${JVM_ARGS} ${GRAPHITE_ARGS} -Dfile.encoding=UTF-8 \
	             -jar ${JAR_FILE} \
	             --spring.config.location=${COMPONENT_HOME}/conf/ \
	             --logging.config=${LOG_CONFIG_FILE} \
	             --logging.path=${LOG_PATH} > /dev/null 2>&1 &

	echo -e "Starting service "${COMPONENT_NAME}" ...\c"
	
	COUNT=0
	MAX_COUNT=0
	while [[ $COUNT -lt 1 ]]; do
		echo -e '.\c'
		sleep 1
		COUNT=`ps --no-heading -C java -f --width 1000 |grep 'proc_name='${COMPONENT_NAME} | awk '{print $2}' | wc -l`
		if [ $COUNT -gt 0 ]; then
			break
		fi
		((MAX_COUNT++))
		if [ ${MAX_COUNT} -eq 30 ];then
			echo "Fail!"
			exit 1
		fi
	done
	echo "OK!"
}

stop(){
	PIDS=`ps -ef|grep 'proc_name='${COMPONENT_NAME} | grep -v grep|awk '{print $2}'`
	echo -e 'Stopping the service '${COMPONENT_NAME}' ...\c'
	for pid in $PIDS; do
		kill $pid > /dev/null 2>&1
	done
	COUNT=0
	while [[ $COUNT -lt 1 ]]; do
		echo -e ".\c"
		COUNT=1
		MAX_COUNT=0
		FORCE_STOP=0
		for PID in $PIDS ; do
			PID_EXIST=`ps --no-heading -p $PID`
			if [ -n "$PID_EXIST" ]; then
				COUNT=0
				if [ ${FORCE_STOP} -eq 0 ];then
					kill $PID > /dev/null 2>&1
				else
					echo "Force kill pid: $PID"
					kill -9 $PID > /dev/null 2>&1
				fi
				break
			fi
		done
		((MAX_COUNT++))
		if [ ${MAX_COUNT} -eq 30 ];then
			FORCE_STOP=1
		fi
		sleep 1
	done
	echo "OK!"
}

# control service based on the first arg.
case $1 in
	start )
		start;;
	stop )
		stop;;
	restart )
		stop
		sleep 3
		start;;
	status )
		status;;
	* )
		echo "Usage: $0 (start|stop|restart|status)";;
esac
