#FROM golang:1.16.3
FROM golang:1.16-alpine

WORKDIR /src/app/fullcycleservice

COPY . /src/app

ENTRYPOINT ["go", "run", "main.go"]
