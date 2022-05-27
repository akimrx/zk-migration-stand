# Intro

* Create two Zookeeper clusters with (6 nodes)
* Create two Clickhouse clusters (4 nodes)
* Connect Clickhouse to one ZK cluster
* Start writing data to Clickhouse
* Change ZK cluster for two Clickhouse nodes



# Autorun

```shell
# Install docker
sudo apt update
sudo apt install docker.io docker-compose -y


# Prepare stand
cd zk-migration-stand
./stand prepare


# Prepare python script for datawrite
python3 -m venv venv
source venv/bin/activate
pip3 install -r requirements.txt

# Run datawriter script
./datawriter


# Wait for 1 min and change ZK cluster for CH cluster (ch03, ch04)
./stand ch updated

# Restore replication for CH cluster with new ZK
./stand ch restore

# Check CH clusters state
./stand ch check


# Check that everything went as expected and delete stand
./stand cleanup

# Optional
docker system prune -f
docker volume prune -f
```

