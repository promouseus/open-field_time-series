# syntax=docker/dockerfile:1
# Bases on: https://github.com/apache/iotdb/tree/master/docker/src/main
FROM apache/iotdb:0.12.0-node
#COPY . /app
#RUN make /app
#CMD python /app/app.py

# sbin/start-cli.sh -h 127.0.0.1 -p 6667 -u root -pw root -e "SET STORAGE GROUP TO root.open_field"
# CREATE TIMESERIES root.open_field.status WITH DATATYPE=BOOLEAN, ENCODING=PLAIN
# CREATE TIMESERIES root.open_field.temperature WITH DATATYPE=FLOAT, ENCODING=RLE
# sbin/start-cli.sh -h 127.0.0.1 -p 6667 -u root -pw root -e "INSERT INTO root.open_field(timestamp,status,temperature) values(`date +%s%3N`,false,`ping 8.8.8.8 -qc1|tail -n 1|awk -F' ' '{print $4}'|awk -F'/' '{print $1}'`)"
