# Helm Chart Repository

This repository contains Helm charts for deploying applications.

## Adding the Repository

```bash
helm repo add my-charts https://[YOUR_GITHUB_USERNAME].github.io/helm-chart3
helm repo update
```

## Installing the Chart

```bash
helm install my-release my-charts/my-chart
```

## Configuration

The following table lists the configurable parameters of the chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `1` |
| `image.repository` | Image repository | `nginx` |
| `image.tag` | Image tag | `latest` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |

## Development

To make changes to the chart:

1. Make your changes in the `my-chart` directory
2. Commit and push to the main branch
3. The GitHub Action will automatically create a new release and update the index

## License

MIT
