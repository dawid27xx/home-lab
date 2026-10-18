# Home Lab

A personal Kubernetes home lab for experimenting with container orchestration, networking, monitoring, and infrastructure tooling.

## Tech Stack

- **Kubernetes:** k3d (k3s running in Docker)
- **Helm:** Upstream charts and configuration templating
- **Kustomize:** Manifest composition and custom resources
- **Make:** Local build and deployment automation
- **Traefik:** Kubernetes ingress controller

## Cluster

The cluster consists of three Kubernetes nodes:

- 1 control-plane node
- 2 worker nodes

Running locally using Docker Desktop and WSL2.

## Services

| Service | Description | Status |
|---|---|---|
| NGINX | Web server deployed using the Bitnami Helm chart | Running |
| Prometheus & Grafana | Cluster monitoring and observability | Planned |
| Cilium | Kubernetes networking and network policies | Planned |

## Deployment Workflow

Each service has its own configuration and Makefile.

```text
Helm Chart + Values
        |
        v
    helm template
        |
        v
  Rendered Manifests
        |
        v
     Kustomize
        |
        v
    Final Manifest
        |
        v
    kubectl apply
        |
        v
  Kubernetes Cluster
```

### Deploying a service

For example, NGINX:

```bash
cd kubernetes/services/nginx

make render  # Render Helm templates
make build   # Generate final manifests using Kustomize
make deploy  # Apply manifests to the cluster
make clean   # Remove generated manifests
```

Namespaces must exist before deploying namespaced resources.

## Goals

- Replicate production-style Kubernetes deployment workflows
- Experiment with ingress, networking, and network policies
- Implement monitoring and alerting using Prometheus and Grafana
- Explore service reliability, scaling, and observability

## Notes

This is a learning environment running on local hardware, not a production cluster.