# build onionize container
FROM alpine:latest
MAINTAINER "Moritz Bartl <moritz@torservers.net>"

ENV DOCKER_HOST unix:///tmp/docker.sock

RUN apk -U --no-progress upgrade \
 && apk -U --no-progress add tor supervisor

COPY files/binary/docker-gen /usr/local/bin/docker-gen
RUN chmod +x /usr/local/bin/docker-gen
COPY files/supervisor/supervisord.conf /etc/supervisor/supervisord.conf
COPY files/docker-gen/torrc.tmpl /app/torrc.tmpl
COPY files/torrc.minimal /etc/torrc

RUN mkdir -p /var/lib/tor/onion_services && \
    chown -R tor /var/lib/tor/onion_services

VOLUME ["/var/lib/tor/"]

ENTRYPOINT ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
