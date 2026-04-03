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

- **Container Registry**: [https://www.cleanstart.com/](https://www.cleanstart.com/)
- **CleanStart Community Images**: [https://hub.docker.com/u/cleanstart](https://hub.docker.com/u/cleanstart)
- **How-to-Run CleanStart images & sample projects**: [https://github.com/cleanstart-containers](https://github.com/cleanstart-containers)
  - How to run sample projects using Dockerfile
  - How to deploy via Kubernetes YAML
  - How to migrate from public images to CleanStart images

---

**Vulnerability Disclaimer**

CleanStart offers Docker images that include third-party open-source libraries and packages maintained by independent contributors. While CleanStart maintains these images and applies industry-standard security practices, it cannot guarantee the security or integrity of upstream components beyond its control.

Users acknowledge and agree that open-source software may contain undiscovered vulnerabilities or introduce new risks through updates. CleanStart shall not be liable for security issues originating from third-party libraries, including but not limited to zero-day exploits, supply chain attacks, or contributor-introduced risks.

Security remains a shared responsibility: CleanStart provides updated images and guidance where possible, while users are responsible for evaluating deployments and implementing appropriate controls.
