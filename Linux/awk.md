# Awk

```
按:号分割，并取第1和第3列
awk -F ':' '{print $1 $3}'

求平均值
cat data | awk '{sum+=$1} END {print sum/NR}'

内置变量
NF：每一行拥有的字段总数
NR：目前处理的行数
FS：目前使用的分隔符


$1: 第1列的内容
$NF: 最后一列的内容
length($NF) : 最后一列内容的长度
```


## 案例1
```
[cloud-user@kafka-3(MS) ~]$ sudo /opt/kafka/bin/kafka-topics.sh --describe --zookeeper `hostname`:2181/kafka --topic 4028834c598ba88401598cb8fe130018.FMS.TELEMATICS.STATUS | awk -F':' '{if(NR==1){hd="STATUS"}else{if(length($NF)==6){hd="OK"}else{hd="ERROR"}};print hd,$0}'
STATUS Topic:4028834c598ba88401598cb8fe130018.FMS.TELEMATICS.STATUS              PartitionCount:9             ReplicationFactor:3        Configs:
ERROR Topic: 4028834c598ba88401598cb8fe130018.FMS.TELEMATICS.STATUS              Partition: 0         Leader: 2            Replicas: 1,2,3   Isr: 2,3
OK         Topic: 4028834c598ba88401598cb8fe130018.FMS.TELEMATICS.STATUS              Partition: 1         Leader: 2            Replicas: 2,3,1   Isr: 2,1,3
OK         Topic: 4028834c598ba88401598cb8fe130018.FMS.TELEMATICS.STATUS              Partition: 2         Leader: 3            Replicas: 3,1,2   Isr: 3,2,1
ERROR Topic: 4028834c598ba88401598cb8fe130018.FMS.TELEMATICS.STATUS              Partition: 3         Leader: 3            Replicas: 1,3,2   Isr: 3,2
OK         Topic: 4028834c598ba88401598cb8fe130018.FMS.TELEMATICS.STATUS              Partition: 4         Leader: 2            Replicas: 2,1,3   Isr: 2,1,3
OK         Topic: 4028834c598ba88401598cb8fe130018.FMS.TELEMATICS.STATUS              Partition: 5         Leader: 3            Replicas: 3,2,1   Isr: 3,2,1
ERROR Topic: 4028834c598ba88401598cb8fe130018.FMS.TELEMATICS.STATUS              Partition: 6         Leader: 2            Replicas: 1,2,3   Isr: 2,3
OK         Topic: 4028834c598ba88401598cb8fe130018.FMS.TELEMATICS.STATUS              Partition: 7         Leader: 2            Replicas: 2,3,1   Isr: 2,1,3
OK         Topic: 4028834c598ba88401598cb8fe130018.FMS.TELEMATICS.STATUS              Partition: 8         Leader: 3            Replicas: 3,1,2   Isr: 3,2,1

```