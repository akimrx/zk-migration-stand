
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

./datawriter

# Wait for 10 min
./stand autotest


# Check that everything went as expected
./stand cleanup


# Optional
docker system prune -f
docker volume prune -f
```

