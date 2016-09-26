## Environment Variables

* DF_SERVICE_PATH

## Test

```bash
docker swarm init

docker service create --name util-1 \
    -l DF_NOTIFY=true \
    -l DF_servicePath=/demo \
    alpine sleep 1000000000

docker service create --name util-2 alpine sleep 1000000000

go test --cover

go build -v -o docker-flow-swarm-listener

DF_INTERVAL=1 DF_NOTIFICATION_URL=http://localhost ./docker-flow-swarm-listener

docker service rm util
```

## TODO

- [ ] Send a remove request to the proxy if a service is removed
- [ ] Ability to have multiple notification addresses
- [ ] Add filters
- [ ] Create a service during test setup
- [ ] Remove the service after tests
- [ ] Add the option to use NewEnvClient
- [ ] Resend requests until the response is 200
- [ ] Functional tests
- [ ] Integration tests
- [ ] Write README
- [ ] Register in CircleCI
- [ ] Ability to initiate service notifications through HTTP (speed up waiting period)