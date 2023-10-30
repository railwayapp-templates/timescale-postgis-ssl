# SSL-enabled Postgres DB image + TimescaleDB and PostGIS

This repository contains the logic to build SSL-enabled Postgres images with TimescaleDB and PostGIS extensions already installed.

When you deploy the TimescaleDB + PostGIS DB service from the Railway-published template, the image that is used is built from this repository.

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.app/template/timescaledb-postgis)

### Why though?

The (timescale/timescaledb-ha)[https://hub.docker.com/r/timescale/timescaledb-ha] image in Docker hub does not come with SSL baked in.

Since this could pose a problem for applications or services attempting to connect, we decided to roll our own image with SSL enabled.

### How does it work?

The Dockerfiles contained in this repository start with the `timescale/timescaledb-ha` image as base.  Then the `init-ssl.sh` script is copied into the `docker-entrypoint-initdb.d/` directory to be executed upon initialization.

#### Cert expiry
By default, the cert expiry is set to 820 days.  You can control this by configuring the `SSL_CERT_DAYS` environment variable as needed.

### A note about running these images locally

These images do not contain support for ARM.  Check out the Dockerfiles that build these images and feel free to copy the logic to build your own image with the appropriate base image containing support for ARM.