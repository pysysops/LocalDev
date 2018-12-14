# LocalDev

Getting fed up of polluting my laptops with every database, queue and datastore
on the internet with `brew`, website downloads or `macports`... I've put them
all in one Docker Compose file and given them reasonable defaults.

## Pre-requisites
Install Docker: https://docs.docker.com/install/

## Components
Below are the various components that run

### MySQL
A Percona 5.7 container with: `utf8mb4` as default, `sql_mode` a little less
restrictive: `NO_ENGINE_SUBSTITUTION` and slow query logging.

Default user: `root` password: `pa55w0rd`
_Don't use root user for applications in production_

### RabbitMQ
A rabbitmq server with management interface.

Default user: `guest` password: `guest`
_Always remove the guest user in production and use application specific users_

### Redis
A redis container with `--appendonly yes`.

_Consider enabling and using auth in production or listening on 127.0.0.1 only_

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
docker-compose up mysql -d
```

### Stop everything
To stop all components and cleanup the containers and networks: 
```
docker-compose down
```

## More info
Docker Compose has fabulous documentation:
https://docs.docker.com/compose/overview/
