# LocalDev

Getting fed up of polluting my laptops with every database, queue and datastore
on the internet with `brew`, website downloads or `macports`... I've put them
all in one Docker Compose file, given them reasonable defaults and wherever
possible configured mounted volumes for persistence.

## Pre-requisites
* Install Docker: https://docs.docker.com/install/
* Increase Docker's memory to 4GB https://docs.docker.com/docker-for-mac/#advanced

## Components
Below are the various components that run and useful information about them.

### [Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started.html)
Elasticsearch `6.5.3` running with `-Xms256m -Xmx256m` and `xpack.security.enabled=false`

#### Web UI
Kibana is running on: http://localhost:5601

_It's worth considering xpack security or basic auth in production_

### [Jaeger](https://www.jaegertracing.io/)
A container running Jaeger for application tracing. Ports are configured for both
Jaeger and Zipkin collectors including http. Personally, I would always recommend
making use of a Jaeger library and sending metrics to a UDP (stateless) collector.

Web UI: http://localhost:16686

### [Minio](https://docs.minio.io/)
A container running as S3 compatible object store.

Access key: `minio` secret key: `minio123`

#### Web UI
You can access the web interface at http://127.0.0.1:9000 using the above
credentials.

### [MySQL](https://www.percona.com/doc/percona-server/LATEST/index.html)
A Percona 5.7 container with: `utf8mb4` as default, `sql_mode` a little less
restrictive: `NO_ENGINE_SUBSTITUTION` and slow query logging.

Default user: `root` password: `pa55w0rd`

_Don't use root user for applications in production_

### [NATS](https://nats.io/documentation/)
A nats server.

#### Web UI
There is an instance of natsboard running at: http://localhost:18222

### [RabbitMQ](https://www.rabbitmq.com/documentation.html)
A rabbitmq server with management interface.

Default user: `guest` password: `guest`

_Always remove the guest user in production and use application specific users_

#### Web UI
The RabbitMQ Management UI is at: http://localhost:15672

### [Redis](https://redis.io/documentation)
A redis container with `--appendonly yes`.

_Consider enabling and using auth in production or listening on 127.0.0.1 only_

#### Web UI
There is a container running Redis Commander at: http://localhost:16379

## Usage
Clone this repo somewhere and open a terminal inside it.

### Start all containers
To start all the containers in the foreground, type:
```
docker-compose up
```
`Ctrl+C` will stop the containers.

To start them in the background, type:
```
docker-compose up -d
```

### Start a single component
To start a single component for example `mysql` in the foreground, type:
```
docker-compose up mysql
```

as above, add the `-d` flag to run it in the background:
```
docker-compose up -d mysql
```

### Stop everything
To stop all components and cleanup the containers and networks:
```
docker-compose down
```

## More info
Docker Compose has fabulous documentation:
https://docs.docker.com/compose/overview/
