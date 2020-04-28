SHELL=/bin/sh

org=stuvie
image=coredns
rel=latest
tag=$(org)/$(image):$(rel)

dnsServer=localhost
dnsProxy=localhost
dnsServer=pie
dnsProxy=ops

default:
	@ echo targets are: build, run, test, push, help, clean

build:
	docker build --network host -t $(tag) -f Dockerfile .

run:
	# docker run --rm -t --name dnsdist -v `pwd`/dnsdist.conf:/etc/dnsdist/dnsdist.conf -p 8870:80 -p 9973:53/tcp -p 9973:53/udp uniplug/dnsdist-docker
	docker-compose up

diag:
	open http://localhost:8870/
	open http://localhost:9961/health

test:
	dig +short @$(dnsServer) -p 5553 server.test.com
	dig +short @$(dnsProxy) -p 9953 coredns.test.com
	dig +short @$(dnsProxy) -p 9963 coretcp.test.com
	dig +short @$(dnsProxy) -p 9973 dnsdist.test.com
	dig +short @$(dnsProxy) -p 9983 dnsdistpp.test.com

push:
	docker image push $(tag)

help:
	docker run --rm -it --name $(image) --net host $(tag) --help

clean:
	docker run --rm -it --name $(image) --net host $(tag)
