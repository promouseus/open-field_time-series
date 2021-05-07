# syntax=docker/dockerfile:1
FROM maven:3-openjdk-11-slim AS builder
ENV version=v0.12.0
WORKDIR /
RUN apt-get -q update; apt-get -qq install git \
    && git clone https://github.com/apache/iotdb.git --branch ${version} \
    && cd iotdb \
    && mvn --quiet clean package -pl grafana -am -Dmaven.test.skip=true

FROM openjdk:11-jre-slim
RUN apt-get -q update; apt-get -qq install curl
WORKDIR /iotdb-grafana
COPY --from=builder /iotdb/grafana/target/iotdb-grafana-*.war iotdb-grafana.war
# https://docs.docker.com/engine/reference/builder/#healthcheck
EXPOSE 8888
HEALTHCHECK --interval=10s --timeout=3s \
  CMD curl -f http://localhost:8888/ || exit 1
ENTRYPOINT ["java" , "-jar", "iotdb-grafana.war"]