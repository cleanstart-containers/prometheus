## Container Documentation for Prometheus Documentation

The CleanStart Prometheus image provides a production-ready, security-hardened container optimized for enterprise environments. Built on a minimal base OS with comprehensive security hardening, this image delivers reliable application execution with advanced security features.

📌 **Base Foundation**: Production-ready container from cleanstart.

**Image Path**: `ghcr.io/cleanstart-containers/prometheus`

**Registry**: cleanstart Registry

## Pull Latest Image
Download the container image from the registry

```bash
docker pull ghcr.io/cleanstart-containers/prometheus:latest
```
```bash
docker pull ghcr.io/cleanstart-containers/prometheus:latest-dev
```

# Basic Run

```bash
docker run -it --name prometheus \
  --entrypoint sh \
  ghcr.io/cleanstart-containers/prometheus:latest-dev \
  -c "mkdir -p /tmp/prometheus && \
      /usr/bin/prometheus \
      --config.file=/etc/prometheus/prometheus.yml \
      --storage.tsdb.path=/tmp/prometheus"
```

# Production Deployment

```bash
docker run -d --name prometheus-prod \
  --security-opt=no-new-privileges \
  --user 1000:1000 \
  --restart unless-stopped \
  --entrypoint sh \
  ghcr.io/cleanstart-containers/prometheus:latest-dev \
  -c "mkdir -p /tmp/prometheus && \
      /usr/bin/prometheus \
      --config.file=/etc/prometheus/prometheus.yml \
      --storage.tsdb.path=/tmp/prometheus"
```

# Volume Mount
/tmp/prometheus should be executable to run this in local machine

```bash
docker run --name prometheus-vol \
  -v /tmp/prometheus:/tmp/prometheus \
  --entrypoint sh \
  ghcr.io/cleanstart-containers/prometheus:latest-dev \
  -c "mkdir -p /tmp/prometheus && \
      /usr/bin/prometheus \
      --config.file=/etc/prometheus/prometheus.yml \
      --storage.tsdb.path=/tmp/prometheus"
```

# Port Forwarding

```bash
docker run --name prometheus-port \
  -p 9090:9090 \
  --entrypoint sh \
  ghcr.io/cleanstart-containers/prometheus:latest-dev \
  -c "mkdir -p /tmp/prometheus && \
      /usr/bin/prometheus \
      --config.file=/etc/prometheus/prometheus.yml \
      --storage.tsdb.path=/tmp/prometheus"
```

## Environment Variables
Configuration options available through environment variables

| Variable | Default | Description |
|----------|---------|-------------|
| ENV | production | Environment mode |
| LOG_LEVEL | info | Logging level |

## Kubernetes Security Context
Recommended security context for Kubernetes deployments

```yaml
securityContext:
  allowPrivilegeEscalation: false
  capabilities:
    drop:
    - ALL
  readOnlyRootFilesystem: true
  runAsUser: 1000
  runAsGroup: 1000
```

## Documentation Resources
Essential links and resources for further information
 
**CleanStart Images**: https://images.cleanstart.com/
 
**Community Images**:
**Docker Hub**: https://hub.docker.com/u/cleanstart<br>
**GitHub**: https://github.com/cleanstart-containers<br>
**AWS ECR Public Gallery**: https://gallery.ecr.aws/cleanstart/
 
**Presence on Social Media**:
**Community**: https://www.linkedin.com/groups/18324021/<br>
**YouTube**: https://www.youtube.com/@CleanStartOfficial<br>
 
**Contribute to Container Use Cases**: https://github.com/cleanstart-dev/cleanstart-use-cases/
