# kafka-cluster-docker
通过 docker-compose 快速部署一个开发环境的 kafka cluster

## 集群规划
```shell
zookeeper 3.6
kafka 2.4

3 kafka broker 1 zookeeper
```


## 部署步骤

- 执行 docker-compose 首次启动集群
```shell
HOSTNAME=`hostname` docker-compose -f kafka_1zk_3brokers.yml -p kafka_cluster_dev up -d
```

- 验证宿主机能否正常连接
```shell
# create topic
./kafka-topics.sh --create --partitions 3 --replication-factor 1 --bootstrap-server `hostname`:9092,`hostname`:9093,`hostname`:9094 --topic kafka_test

# list topics
./kafka-topics.sh --list --bootstrap-server `hostname`:9092,`hostname`:9093,`hostname`:9094
kafka_test
```


- 启停集群
```shell
# 启动
docker-compose -p kafka_cluster_dev start

# 停止
docker-compose -p kafka_cluster_dev stop

# 停止并删除 container
docker-compose -p kafka_cluster_dev down
```