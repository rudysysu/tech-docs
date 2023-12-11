#!/bin/bash

# JAVA
if [ "x$JAVA_HOME" != "x" ]; then
  JAVA="$JAVA_HOME/bin/java"
else
  JAVA=java
fi
echo "JAVA: " ${JAVA}

# JVMFLAGS
JVMFLAGS="\
-server \
-Xms256m \
-Xmx512m \
-XX:-UseGCOverheadLimit \
-Dgroup=ECF-DEV \
-Dapp=TRIP-DETECTOR \
-Dinstance=trip-mgmt-1 \
-DgraphiteIp=192.168.1.23"

echo "JVMFLAGS: " ${JVMFLAGS}

# MAIN_CLASS
# MAIN_CLASS=com.ericsson.fms.trip.detector.TripDetectorApp
# echo "MAIN_CLASS: " ${MAIN_CLASS}

# BASE_DIR
BASE_DIR=$( cd "$( dirname "${BASH_SOURCE[0]}" )" && cd .. && pwd )
echo "BASE_DIR: " ${BASE_DIR}

# MAIN_JAR
MAIN_JAR=${BASE_DIR}/lib/trip-detector-1.0-SNAPSHOT.jar
echo "MAIN_JAR: " ${MAIN_JAR}

# CONF_FILE
CONF_FILE=${BASE_DIR}/conf/application.yml
echo "CONF_FILE: " ${CONF_FILE}

# LOG_FILE
LOG_FILE=${BASE_DIR}/conf/logback.xml
echo "LOG_FILE: " ${LOG_FILE}

# DATA_DIR
DATA_DIR=${BASE_DIR}/data
if [ ! -d "$DATA_DIR" ]; then
  mkdir -p "$DATA_DIR"
fi
echo "DATA_DIR: " ${DATA_DIR}

# LOG_DIR
LOG_DIR=${BASE_DIR}/log
if [ ! -d "$LOG_DIR" ]; then
  mkdir -p "$LOG_DIR"
fi
echo "LOG_DIR: " ${LOG_DIR}

# PID_FILE
PID_FILE=${BASE_DIR}/data/pid
if [ -f "$PID_FILE" ]; then
  PID=`cat ${PID_FILE}`
  if [ ! -d /proc/${PID} ]; then
    rm ${PID_FILE}
  fi
fi
echo "PID_FILE: " ${PID_FILE}

# CLASSPATH
for d in "$BASE_DIR"/lib/*.jar
do
   CLASSPATH="$d:$CLASSPATH"
done

# START
if [ -f "$PID_FILE" ]; then
  echo SERVER already running as process ${PID}.
else
  nohup "${JAVA}" -cp "$CLASSPATH" ${JVMFLAGS} -jar ${MAIN_JAR} --spring.config.location=${CONF_FILE} --logging.config=${LOG_FILE} --logging.path=${LOG_DIR} > ${LOG_DIR}/nohup.out 2>&1 &
  PID=$!
  echo "starting..."
  sleep 5
  if [ "x${PID}" != "x" -a -d /proc/${PID} ]; then
    echo "${PID}" > ${PID_FILE}
    echo STARTED
  else
    echo SERVER DID NOT START
    exit 1
  fi
fi
