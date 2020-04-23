FROM alpine:latest

MAINTAINER resyst-it <florian.cauzardjarry@gmail.com>

RUN apk --update add bind

EXPOSE 53

CMD ["named", "-c", "/data/named.conf", "-g", "-u", "named"]
