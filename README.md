[![build status](https://secure.travis-ci.org/FGRibreau/node-amqp-tool.png)](http://travis-ci.org/FGRibreau/node-amqp-tool)
`AMQP-tool` is a cli for importing and/or exporting message from/to an AMQP/RabbitMQ broker.

## Installation

    $ npm install amqp-tool -g

## Usage overview

```
Usage: node ./bin/amqp-tool [options] [-import | -export]

Options:
  --host          host                                                           [default: "localhost"]
  --user, -u      username                                                       [default: "guest"]
  --password, -p  password                                                       [default: "guest"]
  --port          port                                                           [default: 5672]
  --vhost         vhost                                                          [default: "/"]
  --queue, -q     queue's name to work with                                      [required]
  --passive       set it to true if the queue already exist                      [default: true]
  --durable       the queue will survive a borker restart
  --autoDelete    the queue will be deleted when there is no more subscriptions
  --export        export [filename], export queue's content to filename          [default: "stdout"]
  --import        import [filename], export file content into the queue          [default: "stdin"]
  --count         limit the number of message to export/import
  -v, --verbose   verbose mode                                                   [default: false]
  -h, --help      produce this help message
```

### Export the first 5000 messages of a queue
into a file ...

    amqp-tool --host rabbitmq.local -u user -p azerty -q queuetest --count 5000 --export dump.json

... or to `stdout`

    amqp-tool --host rabbitmq.local -u user -p azerty -q queuetest --count 5000 --export > dump.json



### Continuously export a queue into a file

    amqp-tool --host rabbitmq.local -u user -p azerty -q queuetest --export > dump.json



### Import all messages to a queue
from a file...

    amqp-tool --host rabbitmq.local -u user -p azerty -q queuetest --import dump.json

...or from `stdin`

    cat dump.json | amqp-tool --host rabbitmq.local -u user -p azerty -q queuetest --import


### Import the first 10 messages of a file into a queue

    head -n10 500messages.json | amqp-tool --host rabbitmq.local -u user -p azerty -q queuetest --import


### Continuously transfer message between two RabbitMQ Server (just for fun)

    amqp-tool --host rabbitmq1.local -u user -p azerty -q queue1 --export | amqp-tool --host rabbitmq2.local -u user -p azerty -q queue2 --import
