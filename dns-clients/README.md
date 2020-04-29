![automated builds](https://img.shields.io/docker/cloud/automated/franklouwers/flamethrower.svg) ![build passing](https://img.shields.io/docker/cloud/build/franklouwers/flamethrower.svg)


## Docker Image for the Flamethrower DNS testing tool

### What?

Flamethrower is a small, fast, configurable tool for functional testing, benchmarking, and stress testing DNS servers and networks. It supports IPv4, IPv6, UDP and TCP, and has a modular system for generating queries used in the tests.

It was built as an alternative to [dnsperf](https://nominum.com/measurement-tools/), and many of the command line options are compatible.

### Why use it as a Docker image?

Flamethrower requires fairly recent versions of some libraries to work correctly. Configuring those on your system will cause headaches, 100% guaranteed!
This image packages all those dependencies and reduce the complete installation an building process to a single command.

### Usage and quick examples

Current command line options are described with:

```
docker container run --rm -it franklouwers/flamethrower
```

Flame localhost port 53, UDP, maximum speed:
```
flame localhost
```

Flame target, port 5300, TCP:
```
flame -p 5300 -P tcp target.test.com
```

Flame target, port 443, TCPTLS:
```
flame -p 443 -P tcptls target.test.com
```

Flame target with random labels:
```
flame target.test.com -g randomlabel lblsize=10 lblcount=4 count=1000
```

For more examples and details, please see [flamethrower's readme](https://github.com/DNS-OARC/flamethrower/blob/master/README.md).


### License and Copyright

Flamethrower is licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html), 2017-2019 © NSONE, Inc.

This Dockerfile is licensed under the [BSD 2-clause license](https://opensource.org/licenses/BSD-2-Clause), Copyright 2019 Frank Louwers

### Learn more
Github Source: https://github.com/franklouwers/flamethrower-docker

To learn more about FlameThrower, see https://github.com/DNS-OARC/flamethrower
