Foreldrepenger Java baseimage
=====================

Basic Usage
---------------------

Create a `Dockerfile` containing:
```Dockerfile
FROM ghcr.io/navikt/sif-baseimages/java:21

LABEL org.opencontainers.image.source=https://github.com/navikt/k9-sak

# Config
COPY web/target/classes/logback*.xml ./conf/

# Application Container (Jetty)
COPY web/target/lib/*.jar ./lib/
COPY web/target/app.jar ./
```

### Simplestexample
The simplest way of running your app is to create a far jar and copy it into your container as `app.jar`.
Since the default working directory is `/app`, there's no need to specify the path.

```Dockerfile
FROM ghcr.io/navikt/sif-baseimages/java:21
COPY target/my-awesome.jar app.jar
```

## Customisation

The working director is sett to `/app`.
```Dockerfile
WORKDIR /app
```

Custom runtime options may be specified using the environment variable `JAVA_OPTS`.

### Start up scripts

You can add custom behavior to your container by copying `.sh` files
to the `/init-scripts` dir. The files are sourced which means that
you can export environment variables or extend the existing ones like `JAVA_OPTS`.

