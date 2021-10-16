# Intro

* Create two independent Zookeeper clusters, one of 5 hosts, the other of 3 hosts
* Connect to a cluster of 5 Clickhouse hosts
* Start writing data to Clickhouse
* Transfer data from a 5-host cluster to a 3-host cluster in the following way:
* Adding 2 Zookeeper hosts from a 3-host cluster to a 5-host cluster, updating the configuration on 7 hosts
* Stopping the remaining host from the 3-host cluster
* Alternately restart the hosts of the old cluster with an interval of about 30 seconds
* Alternately restart two hosts from the "new" cluster with an interval of about 30 seconds
* Waiting for data synchronization in the combined Zookeeper cluster
* Updating the client configuration, which will only lead to two new Zookeeper hosts
* Restart the clients that use Zookeeper and make sure that everything is fine
* Update the configuration of the new 3-host cluster to its original state, so that the cluster eventually consists of 3 hosts again
* Stopping a cluster of 5 hosts
* Reboot the new two hosts with an interval of 10-30 seconds, the last to launch the remaining inactive host
* Make sure that clients can work with Zookeeper
* Add the last cluster host to the client configuration and restart the services


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


# Wait for 10 min
./stand autotest


# Check that everything went as expected and delete stand
./stand cleanup

# Optional
docker system prune -f
docker volume prune -f
```

