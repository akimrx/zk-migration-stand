
# Prepare

0. Update symlinks:
```shell
./switch zk original
./switch ch original
```

1. Up the composition with command:
```shell
docker-compose up -d
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


# After 10 minutes prepare Zookeeper joint

1. Joint Zookeeper clusters:
```shell
./switch zk joint
```


