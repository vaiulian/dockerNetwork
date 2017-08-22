# dockerNetwork
Connect container from inside docker-compose file to standalone container

1. Create a docker container running redis

>$ docker run -d --name rediscontainer -p 6379:6379 redis:latest
 
2. Stop the container

>$ docker stop rediscontainer

3. Create a shared docker network

>$ docker network create redisNetwork

4. Add new rediscontainer to new redisNetwork

>$ docker network connect redisNetwork rediscontainer

5. Start the container

>$ docker start rediscontainer

6. Inside the docker-compose.yml add the newly created network to a service

```
version: '2'
services:
    netopservice:
        build: .
        networks:
            - default
            - redisNetwork
networks:
  redisNetwork:
    external: true
```

7. Start docker-compose

>$ docker-compose up
