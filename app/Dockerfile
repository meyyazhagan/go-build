FROM golang:1.12 AS builder
WORKDIR /go/src/app
COPY . .
RUN go get github.com/go-redis/redis
RUN CGO_ENABLED=0 go build
RUN pwd && ls -lrth

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /go/src/app/app /go/src/app/index.html ./
COPY --from=builder /go/src/app/assets ./assets
RUN pwd && ls -lrth
CMD ["./app"]