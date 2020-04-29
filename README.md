loadtests
=========

Load tests for various network protocols. Requires docker, docker-compose, resperf and dig

	git clone https://github.com/stuvie/loadtests

### DNS Load Tests ###

General assumption is that server, proxy and clients hosts are single-purpose.
 
In `dnsserver`, start up ISC bind and test it

    vi Makefile - to set IP for dnsServer
    docker-compose up
    make test - to verify server is responding

In `dns-lb`, start up CoreDNS and DNSdist and test them

    vi Makefile - to set IP for dnsServer and dnsProxy
    vi Corefile* dnsdist.* - to set IP for dnsServer and dnsProxy
    docker-compose up
    make test  - to verify server and proxies are responding

In `dns-clients` run the load tests

    vi Makefile - to set IP for dnsServer and dnsProxy
    make test  - to verify server and proxies are responding
    make queryfile - creates queryfile for resperf
    make resperf
    make flamethrower


### Credits ###

[Bind9 for Docker on alpine](https://github.com/resyst-it/docker-bind9)

[Flamethrower-docker](https://github.com/franklouwers/flamethrower-docker)

[Example domain zone file](https://www.zytrax.com/books/dns/ch6/mydomain.html)

[baseimage-docker](https://github.com/phusion/baseimage-docker)

[docker-bind with webmin](https://github.com/CosmicQ/docker-bind)
