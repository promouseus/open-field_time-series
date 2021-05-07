# syntax=docker/dockerfile:1
# Bases on: https://github.com/apache/iotdb/tree/master/docker/src/main
FROM grafana/grafana:latest
#COPY . /app
#RUN make /app
#CMD python /app/app.py


ENV GF_AUTH_BASIC_ENABLED=true
ENV GF_SECURITY_ADMIN_PASSWORD=admin
ENV GF_ENABLE_GZIP=true
ENV GF_INSTALL_PLUGINS=grafana-simple-json-datasource
