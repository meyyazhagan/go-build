# Build the source code from golang base image
FROM golang:1.12 AS builder
WORKDIR /go/src/app
COPY . .
RUN go get github.com/go-redis/redis
RUN CGO_ENABLED=0 go build

# Multi-Stage Build - Copy the compiled code to alpine image and build the docker image using it.
FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /go/src/app/app /go/src/app/index.html ./
COPY --from=builder /go/src/app/assets ./assets
CMD ["./app"]