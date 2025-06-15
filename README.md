# Helm Chart Repository

This repository contains Helm charts for deploying applications.

## Adding the Repository

```bash
helm repo add my-charts https://[YOUR_GITHUB_USERNAME].github.io/helm-chart3
helm repo update
```

## Installing the Chart

```bash
# For development environment
helm install my-release my-charts/my-chart --set environment=development

# For production environment
helm install my-release my-charts/my-chart --set environment=production

# Override default image
helm install my-release my-charts/my-chart --set image.repository=my-registry/my-image --set image.tag=v1.0.0
```

## Configuration

The following table lists the configurable parameters of the chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `environment` | Environment type (development/production) | `development` |
| `replicaCount.development` | Number of replicas in development | `3` |
| `replicaCount.production` | Number of replicas in production | `5` |
| `image.repository` | Image repository | `busybox` |
| `image.tag` | Image tag | `stable` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `service.type` | Kubernetes service type | `ClusterIP` |
| `service.ports` | Service ports configuration | See values.yaml |
| `ingress.enabled` | Enable ingress | `true` |
| `ingress.className` | Ingress class name | `nginx` |
| `ingress.hosts` | Ingress hosts configuration | See values.yaml |
| `resources` | Pod resource requests and limits | See values.yaml |
| `spring.profiles` | Spring profiles configuration | See values.yaml |

### Image Configuration

The chart uses `busybox:stable` as the default image, but you can easily override it:

```bash
# Using --set
helm install my-release my-charts/my-chart --set image.repository=my-registry/my-image --set image.tag=v1.0.0

# Using values file
helm install my-release my-charts/my-chart -f custom-values.yaml
```

Example custom-values.yaml:
```yaml
image:
  repository: my-registry/my-image
  tag: v1.0.0
  pullPolicy: Always
```

### Service Ports

The chart exposes three ports:
- 8080: API endpoint (/api)
- 8081: Logs endpoint (/logs)
- 8082: SOAP endpoint (/soap)

### Ingress Configuration

The chart configures different hosts for development and production environments:
- Development: dev.example.local
- Production: example.local

## Development

To make changes to the chart:

1. Make your changes in the `my-chart` directory
2. Update the version in `Chart.yaml`
3. Commit and push to the main branch
4. The GitHub Action will automatically create a new release and update the index

## Current Version

The current version of the chart is `0.2.0`. This version includes:
- Environment-specific configurations
- Rolling update strategy
- Health checks
- Resource management
- ConfigMap and Secret handling
- Graceful shutdown

## License

MIT
