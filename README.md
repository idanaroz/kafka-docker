## Pre-Requisites

1. install docker-compose [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)
2. Clone the project 
3. modify the ```KAFKA_ADVERTISED_HOST_NAME``` variable in [docker-compose-idan.yml] (https://github.com/idanaroz/kafka-docker/blob/master/docker-compose-idan.yml) to match your docker host IP (Note: Do not use localhost or 127.0.0.1 as the host ip if you want to run multiple brokers.)
For example, you can use: 
$ hostname -I | grep -o '^\S*'

4. modify the ```kafka_bootstrapServer``` var in [docker-compose-idan.yml] (https://github.com/idanaroz/kafka-docker/blob/master/docker-compose-idan.yml) to match your docker host IP (same ip as on step 3) with the port 9092 concatenated (Should hold). 
e.g. 192.168.1.21:9092


## Create and run the containers with docker compose
$ (sudo) docker-compose -f docker-compose-idan.yml up

## Containers images
The containers images:
- Kafka and zookeeper images was taken from docker hub ( https://hub.docker.com/r/wurstmeister/zookeeper/ , https://github.com/wurstmeister/kafka-docker)

- Kafka producer service was created: https://github.com/idanaroz/kafka-producer . Its image was uploaded to docker hub: https://cloud.docker.com/u/idanaroz/repository/docker/idanaroz/kafka-server-producer

- Kafka consumer worker was created: https://github.com/idanaroz/kafka-consumer . Its image was uploaded to docker hub: https://cloud.docker.com/u/idanaroz/repository/docker/idanaroz/kafka-consumer


## Notes

# Send message via Producer service
` curl -X POST \
  http://<KAFKA_ADVERTISED_HOST_NAME>:8080/produce \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 54bdf002-bc1e-c318-2886-5f126c2cccf9' \
  -d '"Message content"'`

# Connect to running container
 ``` sudo docker exec -it "<container-id>" sh ```
 
