SHELL=/bin/sh

org=stuvie
image=flamethrower
rel=latest
tag=$(org)/$(image):$(rel)

default:
	@ echo targets are: build, run, test, push, help, clean

build:
	docker build --network host -t $(tag) -f Dockerfile .

run:
	docker run --rm -it --name $(image) --net host $(tag) -t 5 -l 10 -v 1 -p 53 localhost
	echo next you should run: make dnsdist

dnsdist:
	docker run --rm -it --name $(image) --net host $(tag) -t 5 -l 10 -v 1 -p 9973 localhost
	echo next you should run: make coredns

coredns:
	docker run --rm -it --name $(image) --net host $(tag) -t 5 -l 10 -v 1 -p 9953 localhost
	echo next you should run: make coretcp

coretcp:
	docker run --rm -it --name $(image) --net host $(tag) -t 5 -l 10 -v 1 -p 9963 localhost
	
test:
	dig +short @localhost server.test.com
	dig +short @localhost -p 9953 coredns.test.com
	dig +short @localhost -p 9963 coretcp.test.com
	dig +short @localhost -p 9973 dnsdist.test.com
	docker run --rm -it --name $(image) -v `pwd`/data:/data --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 3 -p 9953 localhost -f /data/queries
	docker run --rm -it --name $(image) -v `pwd`/data:/data --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 3 -p 9963 localhost -f /data/queries
	docker run --rm -it --name $(image) -v `pwd`/data:/data --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 3 -p 9973 localhost -f /data/queries

push:
	docker image push $(tag)

help:
	docker run --rm -it --name $(image) --net host $(tag) --help

clean:
	docker run --rm -it --name $(image) --net host $(tag)
