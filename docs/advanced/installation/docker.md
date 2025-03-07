# Install Source++ with Docker or Docker Compose

You can install Source++ with Docker or Docker Compose if you are evaluating, testing, or developing Source++.
For production, we recommend installing with Kubernetes.

## Prerequisites

- [Docker](https://docs.docker.com/install)
- [Docker Compose](https://docs.docker.com/compose/install) (optional, only needed for the Docker Compose install method)

## Install with Docker

Run the following commands in your command line.

### spp-platform network

```bash
docker network create spp-platform
```

### Source++ Platform
```bash
docker run --name spp-platform --restart always -p 12800:12800 -d --network spp-platform -e SPP_OAP_HOST=skywalking -e SPP_DISABLE_TLS=true -e SPP_DISABLE_JWT=true -it sourceplusplus/spp-platform:latest
```

### Apache SkyWalking (incl. Source++ processors)
```bash
docker run --name skywalking-oap --restart always -d --network spp-platform -e SPP_PLATFORM_HOST=spp-platform -e SPP_PLATFORM_PORT=5460 -e SPP_DISABLE_TLS=true -it sourceplusplus/spp-oap-server:latest
```

Navigate to http://localhost:12800/stats to view the metrics and http://localhost:12800/health for readiness.

## Install with Docker Compose

Run the following commands in your command line.

```bash
wget https://raw.githubusercontent.com/sourceplusplus/live-platform/main/docker/docker-compose.yml
docker-compose -f docker-compose.yaml up
```
