
# Prepare

1. Prepare the environment and launch the containers:
```shell
./stand prepare
```

2. Checkout the composition:
```shell
docker ps --format "table {{.Names}}\t{{.Image}}\t{{.Status}}
docker-compose logs -f --tail 50
```

3. Create database and table in the Clickhouse:
```shell
./init-ch
```

4. Run the datawriter script:
```shell
./datawriter
```


# After 10 minutes, prepare Zookeeper merged cluster

1. Joint Zookeeper clusters:
```shell
./stand zk joint
```

2. Find the Zookeeper leader:
```shell
./stand leader
```

3. Stop zzz3 container. Restart the containers one by one with 10 sec interval, first the subscribers of the old cluster, then the leader of the old cluster, then the two attached containers

4. Check updated Zookeeper cluster. There should be 5 hosts in the cluster and no errors.

5. Change Clickhouse config:
```shell
./stand ch updated
docker restart ch01
```

6. Switch Zookeeper configs to original:
```shell
./stand zk original
```

7. Stop all old containers with Zookeeper:
```shell
docker stop zoo1 zoo2 zoo3
```

8. Restart new containers and start idle ZK node:
```shell
docker restart zzz1 zzz2
# wait 10-20 sec
docker start zoo3
```

9. All done.
