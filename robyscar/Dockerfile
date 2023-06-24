#   20260624 update
#   ITs$B v.1.00
#

#   FROM python:3.10-alpine
#   docker run --name python-apline -it python:3.11.4-alpine3.18 /bin/sh

FROM python:3.11.4-alpine3.18

# create a non-privileged user to use at runtime
RUN addgroup -g 50 -S pgadmin \
 && adduser -D -S -h /pgadmin -s /sbin/nologin -u 1000 -G pgadmin pgadmin \
 && mkdir -p /pgadmin/config /pgadmin/storage /var/log/pgadmin /var/lib/pgadmin \
 && chown -R 1000:50 /pgadmin \
 && chown -R 1000:50 /var/log/pgadmin \
 && chown -R 1000:50 /var/lib/pgadmin

# Install postgresql tools for backup/restore
RUN apk update \
 && apk add --no-cache libedit postgresql wget \
 && cp /usr/bin/psql /usr/bin/pg_dump /usr/bin/pg_dumpall /usr/bin/pg_restore /usr/local/bin/ \
 && apk del postgresql

RUN apk add --no-cache postgresql-dev libffi-dev zlib-dev jpeg-dev

#   ENV PGADMIN_VERSION=7.0
ENV PGADMIN_VERSION=7.3

ENV PYTHONDONTWRITEBYTECODE=1
ENV CRYPTOGRAPHY_DONT_BUILD_RUST=1

#   echo "https://pgadmin-archive.postgresql.org/pgadmin4/v$7.3/pip/pgadmin4-7.3-py3-none-any.whl" | pip install --no-cache-dir -r /dev/stdin \


### / # echo "https://pgadmin-archive.postgresql.org/pgadmin4/v$7.3/pip/pgadmin4-7.3-py3-none-any.whl" | pip install ### --no-cache-dir -r /dev/stdin \
###     > 
### Collecting pgadmin4==7.3 (from -r /dev/stdin (line 1))
### ERROR: HTTP error 403 while getting https://pgadmin-archive.postgresql.org/pgadmin4/v.3/pip/pgadmin4-7.3-py3-none-any.whl
### ERROR: Could not install requirement pgadmin4==7.3 
### from https://pgadmin-archive.postgresql.org/pgadmin4/v.3/pip/pgadmin4-7.3-py3-none-any.whl 
### (from -r /dev/stdin (line 1)) 
### because of HTTP error 403 Client Error: Forbidden for 
### url: https://pgadmin-archive.postgresql.org/pgadmin4/v.3/pip/pgadmin4-7.3-py3-none-any.whl 
### for URL https://pgadmin-archive.postgresql.org/pgadmin4/v.3/pip/pgadmin4-7.3-py3-none-any.whl


RUN apk add --no-cache alpine-sdk linux-headers \
 && pip install --upgrade pip \
 && echo "https://pgadmin-archive.postgresql.org/pgadmin4/v${PGADMIN_VERSION}/pip/pgadmin4-${PGADMIN_VERSION}-py3-none-any.whl" | pip install --no-cache-dir -r /dev/stdin \
 && pip install --no-cache-dir --upgrade Flask-WTF==0.14.3 \
 && pip install simple-websocket \
 && apk del alpine-sdk linux-headers

EXPOSE 5050

### /usr/local/lib/python3.11/site-packages/pgadmin4/config_distro.py

#   COPY config_distro.py /usr/local/lib/python3.10/site-packages/pgadmin4/
COPY config_distro.py /usr/local/lib/python3.11/site-packages/pgadmin4/

USER pgadmin:pgadmin

### /usr/local/lib/python3.11/site-packages/pgadmin4/pgAdmin4.py

#   CMD ["python", "./usr/local/lib/python3.10/site-packages/pgadmin4/pgAdmin4.py"]
CMD ["python", "./usr/local/lib/python3.11/site-packages/pgadmin4/pgAdmin4.py"]

VOLUME /pgadmin/
