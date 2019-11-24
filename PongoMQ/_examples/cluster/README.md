# pongo cluster example

This will start a local three node cluster.

## Build

```bash
$ go get wx.pongo/...
$ cd $GOPATH/src/wx.pongo/cmd/pongo
$ go build
```

## Start the nodes

```bash
$ ./pongo broker \
          --data-dir="/tmp/pongo0" \
          --broker-addr=127.0.0.1:9001 \
          --raft-addr=127.0.0.1:9002 \
          --serf-addr=127.0.0.1:9003 \
          --bootstrap \
          --bootstrap-expect=3 \
          --id=1

$ ./pongo broker \
          --data-dir="/tmp/pongo1" \
          --broker-addr=127.0.0.1:9101 \
          --raft-addr=127.0.0.1:9102 \
          --serf-addr=127.0.0.1:9103 \
          --join=127.0.0.1:9003 \
          --bootstrap-expect=3 \
          --id=2

$ ./pongo broker \
          --data-dir="/tmp/pongo2" \
          --broker-addr=127.0.0.1:9201 \
          --raft-addr=127.0.0.1:9202 \
          --serf-addr=127.0.0.1:9203 \
          --join=127.0.0.1:9003 \
          --bootstrap-expect=3 \
          --id=3
```

## docker-compose cluster

To start a [docker compose](https://docs.docker.com/compose/) cluster use the provided `docker-compose.yml`.
