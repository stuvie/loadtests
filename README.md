loadtests
=========

Load tests for various network protocols. Requires docker

	git clone https://github.com/stuvie/loadtests

### DNS Load Tests ###

In `dnsserver`, start up ISC bind and test it

    docker-compose up
    make test

In `dns-lb`, start up CoreDNS and DNSdist and test them

    docker-compose up
    make test

In `flamethrower` run the load test

    make run


### Credits ###

[Bind9 for Docker on alpine](https://github.com/resyst-it/docker-bind9)

[Flamethrower-docker](https://github.com/franklouwers/flamethrower-docker)

[Example domain zone file](https://www.zytrax.com/books/dns/ch6/mydomain.html)

[baseimage-docker](https://github.com/phusion/baseimage-docker)

[docker-bind with webmin](https://github.com/CosmicQ/docker-bind)
