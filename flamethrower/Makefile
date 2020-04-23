SHELL=/bin/sh

org=stuvie
image=flamethrower
rel=latest
tag=$(org)/$(image):$(rel)

default:
	@ echo targets are: build, push, help, debug, run, clean

build:
	docker build --network host -t $(tag) -f Dockerfile .

push:
	docker image push $(tag)

help:
	docker run --rm -it --name $(image) --net host $(tag) --help

debug:
	# docker run --rm -it --name $(image) --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 10 8.8.8.8
	docker run --rm -it --name $(image) --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 3 8.8.8.8
	docker run --rm -it --name $(image) -v `pwd`/data:/data --net host $(tag) -t 5 -q 1 -n 1 -c 1 -v 3 8.8.8.8 -f /data/queries

run:
	docker run --rm -it --name $(image) --net host $(tag) -t 5 -l 10 -v 1 localhost

clean:
	docker run --rm -it --name $(image) --net host $(tag) --help
