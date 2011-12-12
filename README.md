## (Work in Progress, will be released through npm soon) ##

## Installation

    $ npm install amqp-tool -g

## Usage overview

```bash
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

### Export the first 5000 messages of a queue into a file

    amqp-tool --host rabbitmq.local -u user -p azerty -q queuetest --export dump.json --count 5000

or

    amqp-tool --host rabbitmq.local -u user -p azerty -q queuetest --export --count 5000 > dump.json


### Continuously export a queue into a file

    amqp-tool --host rabbitmq.local -u user -p azerty -q queuetest --export > dump.json

## TODO
 * Import messages into a queue from a file.json or `stdout`
