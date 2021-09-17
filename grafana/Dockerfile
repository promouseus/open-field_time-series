# syntax=docker/dockerfile:1
FROM debian AS builder
RUN apt-get update; apt-get -y install openssl
# Generated (UNSAFE!) self signed SSL so Grafana can run as TLS/H2 always!
RUN openssl req -nodes -newkey rsa:4096 -x509 -keyout /etc/ssl/private/server.key -out /etc/ssl/private/server.crt -days 3654 -subj "/C=NL/ST=Noord-Holland/L=Zaanstad/O=Promouseus/OU=open-field/CN=open-field.local/emailAddress=noreply@open-field.local"

# Bases on: https://github.com/apache/iotdb/tree/master/docker/src/main
FROM grafana/grafana:latest
COPY iotdb.yaml /etc/grafana/provisioning/datasources/iotdb.yaml
COPY --from=builder --chown=grafana:root /etc/ssl/private/server.* /etc/ssl/private/

ENV GF_DEFAULT_INSTANCE_NAME=open-field_time-series

ENV GF_AUTH_BASIC_ENABLED=true
ENV GF_SECURITY_ADMIN_USER=open-field
ENV GF_SECURITY_ADMIN_PASSWORD=admin1234
#ENV GF_AUTH_ANONYMOUS_ORG_ROLE=Admin
#ENV GF_AUTH_ANONYMOUS_ENABLED=true

ENV GF_SECURITY_DISABLE_GRAVATAR=true
ENV GF_SECURITY_DATA_SOURCE_PROXY_WHITELIST=iotdb-grafana:8888
ENV GF_SECURITY_COOKIE_SECURE=true
ENV GF_SECURITY_COOKIE_SAMESITE=strict

ENV GF_ENABLE_GZIP=true
ENV GF_INSTALL_PLUGINS=grafana-simple-json-datasource
ENV GF_PATHS_TEMP_DATA_LIFETIME=12h

# https://grafana.com/docs/grafana/latest/administration/configuration/
ENV GF_SERVER_PROTOCOL=h2
ENV GF_SECURITY_STRICT_TRANSPORT_SECURITY=true
ENV GF_SECURITY_STRICT_TRANSPORT_SECURITY_MAX_AGE_SECONDS=63072000
ENV GF_SECURITY_STRICT_TRANSPORT_SECURITY_SUBDOMAINS=true
ENV GF_SECURITY_STRICT_TRANSPORT_SECURITY_PRELOAD=true
# https://hstspreload.org/
ENV GF_SERVER_CERT_FILE=/etc/ssl/private/server.crt
ENV GF_SERVER_CERT_KEY=/etc/ssl/private/server.key
