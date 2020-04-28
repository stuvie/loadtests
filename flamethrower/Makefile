SHELL=/bin/sh

org=stuvie
image=flamethrower
rel=latest
tag=$(org)/$(image):$(rel)

dnsServer=localhost
dnsProxy=localhost
dnsServer=fw
dnsProxy=ops

default:
	@ echo targets are: build, run, test, push, help, clean

build:
	docker build --network host -t $(tag) -f Dockerfile .

run:
	docker run --rm -it --name $(image) --net host $(tag) -t 5 -l 10 -v 1 -p 5553 $(dnsServer)
	echo next you should run: make dnsdist

dnsdist:
	docker run --rm -it --name $(image) --net host $(tag) -t 5 -l 10 -v 1 -p 9973 $(dnsProxy)
	echo next you should run: make coredns

coredns:
	docker run --rm -it --name $(image) --net host $(tag) -t 5 -l 10 -v 1 -p 9953 $(dnsProxy)
	echo next you should run: make coretcp

coretcp:
	docker run --rm -it --name $(image) --net host $(tag) -t 5 -l 10 -v 1 -p 9963 $(dnsProxy)
	
test:
	dig +short @$(dnsServer) -p 5553 server.test.com
	dig +short @$(dnsProxy) -p 9953 coredns.test.com
	dig +short @$(dnsProxy) -p 9963 coretcp.test.com
	dig +short @$(dnsProxy) -p 9973 dnsdist.test.com
	echo next you should run: make flametest

flametest:
	docker run --rm -it --name $(image) -v `pwd`/data:/data --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 3 -p 9953 $(dnsProxy) -f /data/queries
	docker run --rm -it --name $(image) -v `pwd`/data:/data --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 3 -p 9963 $(dnsProxy) -f /data/queries
	docker run --rm -it --name $(image) -v `pwd`/data:/data --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 3 -p 9973 $(dnsProxy) -f /data/queries

push:
	docker image push $(tag)

help:
	docker run --rm -it --name $(image) --net host $(tag) --help

clean:
	docker run --rm -it --name $(image) --net host $(tag)
