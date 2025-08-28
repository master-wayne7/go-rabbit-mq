# go-rabbit-mq

Simple example showing how to send and receive messages with RabbitMQ using Go and the `github.com/rabbitmq/amqp091-go` client.

Files in this repo:
- [docker-compose.yml](docker-compose.yml)
- [go.mod](go.mod)
- [send/send.go](send/send.go)
- [receive/receive.go](receive/receive.go)

Quick overview:
- Sender: [`send.main`](send/send.go) sends a single message ("Hello World!") to the `hello` queue using [`send.failOnError`](send/send.go).
- Receiver: [`receive.main`](receive/receive.go) consumes messages from the `hello` queue and logs them using [`receive.failOnError`](receive/receive.go).

Requirements
- Go (see [go.mod](go.mod))
- Docker & Docker Compose

Run locally with Docker Compose
1. Start RabbitMQ:
```sh
docker-compose up -d
```
See configuration in [docker-compose.yml](docker-compose.yml).
2. Wait until RabbitMQ is healthy (healthcheck may take a few seconds):
```sh
docker-compose logs -f rabbitmq
```
Run the receiver (keep this running in one terminal)
```sh
go run ./receive
```
or
```sh
go run [receive.go](receive/receive.go)
```
This runs the code in `receive/main` and will print received messages.

Run the sender (in another terminal)
```sh
go run ./send
```
or
```sh
go run [send.go](send/send.go)
```
This runs the code in send/main and sends a single message.

Build binaries
```sh
go build -o bin/receive ./receive
go build -o bin/send    ./send
```
Troubleshooting

- Connection refused: ensure RabbitMQ is running and ports in docker-compose.yml (5672, 15672) are available.
- Check Docker container status:
```sh
docker ps
docker-compose logs rabbitmq
```
If Go modules are missing dependencies, run:
```sh
go mod tidy
```
See [go.mod](go.mod).