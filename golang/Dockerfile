FROM golang:1.14-alpine AS build
WORKDIR /go/src/github.com/username/go-app-name

ENV CGO_ENABLED=0

RUN apk add --no-cache g++

COPY go.* /go/src/github.com/username/go-app-name/
RUN go mod download

COPY . /go/src/github.com/username/go-app-name/

RUN go test ./... \
    && go build -a -installsuffix cgo -o /go/bin/app-name ./cmd/app-name/main.go

FROM alpine:3.11 AS runtime

COPY --from=build /go/bin/app-name ./

ENTRYPOINT ["./app-name"]