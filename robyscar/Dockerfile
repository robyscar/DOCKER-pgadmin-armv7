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

###     https://pypi.org/project/pgadmin4/
### pip install pgadmin4
###         or
### pip install https://ftp.postgresql.org/pub/pgadmin/pgadmin4/v7.3/pip/pgadmin4-7.3-py3-none-any.whl

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

###     nano /usr/local/lib/python3.11/site-packages/pgadmin4/config_distro.py

USER pgadmin:pgadmin

### /usr/local/lib/python3.11/site-packages/pgadmin4/pgAdmin4.py

#   CMD ["python", "./usr/local/lib/python3.10/site-packages/pgadmin4/pgAdmin4.py"]
CMD ["python", "./usr/local/lib/python3.11/site-packages/pgadmin4/pgAdmin4.py"]

VOLUME /pgadmin/




### docker run --hostname=75665d08bebd --mac-address=02:42:ac:11:00:02 --env=PATH=/usr/local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin --env=LANG=C.UTF-8 --env=GPG_KEY=A035C8C19219BA821ECEA86B64E628F8D684696D --env=PYTHON_VERSION=3.11.4 --env=PYTHON_PIP_VERSION=23.1.2 --env=PYTHON_SETUPTOOLS_VERSION=65.5.1 --env=PYTHON_GET_PIP_URL=https://github.com/pypa/get-pip/raw/0d8570dc44796f4369b652222cf176b3db6ac70e/public/get-pip.py --env=PYTHON_GET_PIP_SHA256=96461deced5c2a487ddc65207ec5a9cffeca0d34e7af7ea1afc470ff0d746207 --restart=no --runtime=runc -t -d python:3.11.4-alpine3.18