###kafka常用命令

```shell
#kafka系统启动
bin/kafka-server-start.sh config/server.properties
#查看kafka主题列表
bin/kafka-topics.sh --list  --zookeeper localhost:2181
#创建一个topic
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic your_topic_name
#查看一个topic的详情
bin/kafka-topics.sh  --zookeeper localhost:2181 --describe --topic your_topic_name
#生产者客户端命令       
bin/kafka-console-producer.sh --brokder-list localhost:9092 --topic your_topic_name
#消费者客户端命令 
bin/kafka-console-consumer.sh --brokder-list localhost:9092 --from-beginning --topic your_topic_name
#删除topic
bin/kafka-topics.sh --zookeeper localhost:2181 --delete --topic your_topic_name
#只是标志删除
```