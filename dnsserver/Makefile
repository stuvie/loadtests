SHELL=/bin/sh

org=stuvie
image=bind9
rel=latest
tag=$(org)/$(image):$(rel)

default:
	@ echo targets are: build, run, test, push, help, clean

build:
	docker build --network host -t $(tag) -f Dockerfile .

run:
	docker-compose up

test:
	dig +short @localhost -p 5553 server.test.com

push:
	docker image push $(tag)

help:
	docker run --rm -it --name $(image) --net host $(tag) --help

clean:
	docker run --rm -it --name $(image) --net host $(tag)
