# pgadmin4 docker image build on RPI 4 - armv7 (32 bit architecture)

This project is entirely inspired by [Benuhx](https://github.com/Benuhx/pgadmin4-docker-arm). Code has been shamelessly copied and a CI/CD pipeline created to automatically build and push images if needed. Images are provided at [dockerhub](https://hub.docker.com/repository/docker/hunnguye/pgadmin4-armv7)

One build on a RPI 4 with 8GB RAM takes around 20 minutes.

An example docker-compose deployment with a postgres DB has been included.

## Access pgadmin UI

To access the webinterface enter `[ip address of your pi]:9090`
* The default email is: test@example.com
* The default password is: 123456

## Access postgres in pgadmin
To add the postgres DB as a server right click on **servers** > **create** > **server...**

Under connection fill in the appropriate credentials:
* Host name: postgres (the name of the postgres container)
* username: pg_user
* password: pg123456

These are set as enviroment variables in the docker-compose and can be changed at will

**! This is just a test setup, make sure to mount volumes to persist data. !**
