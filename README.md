![Helm CI](https://github.com/sandeep9948/helm-k8s-deployment/actions/workflows/helm-ci.yml/badge.svg)

# Kubernetes Deployment with Helm and GitHub Actions

A Helm chart that deploys a web application to Kubernetes, with a GitHub Actions pipeline that lints, renders, and packages the chart automatically.

## Why I Built This
Helm is the standard way to package and deploy applications to Kubernetes. This project demonstrates writing a chart from scratch and validating it through a CI pipeline.

## What Gets Deployed
| Component | Details |
|---|---|
| Deployment | 2 replicas, rolling update strategy |
| Service | ClusterIP, port 80 |
| ConfigMap | Injects environment and log level |

## Project Structure

helm-k8s-deployment/
├── charts/webapp/
│   ├── Chart.yaml           # Chart name, version, description
│   ├── values.yaml          # Default config values
│   └── templates/
│       ├── deployment.yaml  # Pod definition and replicas
│       ├── service.yaml     # Exposes the app inside the cluster
│       └── configmap.yaml   # Environment variables
└── .github/workflows/       # CI pipeline

## CI Pipeline Steps
1. Lint the chart — catches syntax errors
2. Render templates — validates the Kubernetes manifests are valid
3. Package into `.tgz` — ready to be pushed to a Helm registry
4. Upload packaged chart as a build artifact

## How You'd Deploy This to a Real Cluster
```bash
# Install
helm install my-webapp charts/webapp

# Check pods
kubectl get pods

# Upgrade
helm upgrade my-webapp charts/webapp --set replicaCount=3

# Uninstall
helm uninstall my-webapp
```

## Override for Different Environments
```bash
helm install my-webapp charts/webapp \
  --set app.environment=staging \
  --set replicaCount=1
```

## Skills Shown
`Helm` `Kubernetes` `GitHub Actions` `CI/CD` `ConfigMap` `Deployment` `Service`
