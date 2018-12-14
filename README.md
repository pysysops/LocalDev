# LocalDev

Getting fed up of polluting my laptops with every database, queue and datastore
on the internet I've put them all in one Docker Compose file and given them
reasonable defaults.

## MySQL
A Percona 5.7 container with: `utf8mb4` as default, `sql_mode` a little less
restrictive: `NO_ENGINE_SUBSTITUTION` and slow query logging.

Default user: `root` password: `pa55w0rd`
_Don't use root user for applications in production_

## RabbitMQ
A rabbitmq server with management interface.

Default user: `guest` password: `guest`
_Always remove the guest user in production and use application specific users_

## Redis
A redis container with `--appendonly yes`.

_Consider enabling and using auth in production or listening on 127.0.0.1 only_