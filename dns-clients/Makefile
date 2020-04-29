SHELL=/bin/sh

org=stuvie
image=flamethrower
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

flamethrower:
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
	dig +short @$(dnsProxy) -p 9983 dnsdistpp.test.com
	echo next you should run: make flametest

queryfile:
	cp t q
	cat q q q q q q q q q q > qq
	cp qq q
	cat q q q q q q q q q q > qq
	cp qq queryfile
	rm q qq

resperf: queryfile
	echo server test:
	resperf -d queryfile -p 5553 -s $(dnsServer)
	echo coredns test:
	resperf -d queryfile -p 9953 -s $(dnsProxy)
	echo coredns TCP test:
	resperf -d queryfile -p 9963 -s $(dnsProxy)
	echo dnsdist test:
	resperf -d queryfile -p 9973 -s $(dnsProxy)
	echo dnsdist ProxyProtocol test:
	resperf -d queryfile -p 9983 -s $(dnsProxy)

flametest:
	docker run --rm -it --name $(image) -v `pwd`/data:/data --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 3 -p 9953 $(dnsProxy) -f /data/queries
	docker run --rm -it --name $(image) -v `pwd`/data:/data --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 3 -p 9963 $(dnsProxy) -f /data/queries
	docker run --rm -it --name $(image) -v `pwd`/data:/data --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 3 -p 9973 $(dnsProxy) -f /data/queries

push:
	docker image push $(tag)

help:
	docker run --rm -it --name $(image) --net host $(tag) --help

clean:
	rm -f q qq queryfile
	# docker run --rm -it --name $(image) --net host $(tag)
