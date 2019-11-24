FROM golang:1.9-alpine as build-base
RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh make && \
    go get -u github.com/golang/dep/cmd/dep
ADD . /go/src/wx.pongo
WORKDIR /go/src/wx.pongo
RUN GOOS=linux GOARCH=amd64 make build

FROM alpine:latest
COPY --from=build-base /go/src/wx.pongo/cmd/pongo/pongo /usr/local/bin/pongo
EXPOSE 9092 9093 9094 9095
VOLUME "/tmp/pongo"
CMD ["pongo", "broker"]
