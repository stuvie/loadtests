SHELL=/bin/sh

org=stuvie
image=bind9
rel=1.0
tag=$(org)/$(image):$(rel)

dnsServer=pie

default:
	@ echo targets are: build, run, test, push, help, clean

buildx:
	docker buildx ls
	# docker buildx create --name mybuilder
	docker buildx use mybuilder
	docker buildx inspect --bootstrap
	docker buildx ls
	docker buildx build --platform linux/amd64,linux/arm/v7 -t $(tag) --push .
	docker buildx imagetools inspect $(tag)

build:
	docker build --network host -t $(tag) -f Dockerfile .

run:
	docker-compose up

test:
	dig +short @$(dnsServer) -p 5553 server.test.com
	dig +short @$(dnsServer) -p 5553 dnsdistpp.test.com
	dig +short @$(dnsServer) -p 5553 version.bind txt chaos

push:
	docker image push $(tag)

help:
	docker run --rm -it --name $(image) --net host $(tag) --help

clean:
	docker run --rm -it --name $(image) --net host $(tag)
