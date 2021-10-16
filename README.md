
```shell
./stand prepare
./datawriter
# wait for 10 min
./stand autotest
# check that everything went as expected
./stand cleanup

# optional
docker system prune -f
docker volume prune -f
```

