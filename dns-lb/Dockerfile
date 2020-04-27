# Building the binary
FROM golang:1.12 as builder

WORKDIR /go/src

RUN git clone https://github.com/lucashuang97/coredns.git && \
    cd coredns && \
    git checkout BSL-862

ADD plugin.cfg /go/src/coredns/plugin.cfg


WORKDIR /go/src/coredns

#Shouldn't have to do a 'make gen' but if we don't the xpf plugin is not compiled into the executable
RUN make gen
RUN GOOS=linux make

# For the certs
FROM debian:stable-slim as certs

RUN apt-get update && apt-get -uy upgrade

RUN apt-get -y install ca-certificates && update-ca-certificates


# The actual docker image
FROM alpine as production

COPY --from=certs /etc/ssl/certs /etc/ssl/certs
COPY --from=builder /go/src/coredns/coredns /coredns

RUN apk add curl
# ADD Corefile /reverse-dns-proxy-config/Corefile


EXPOSE 9953 9953/udp
EXPOSE 8081
ENTRYPOINT ["/coredns", "-dns.port", "9953", "-conf", "/data/Corefile"]
