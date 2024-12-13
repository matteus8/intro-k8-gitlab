# What is Helm
Helm also populary know as 'a Helm Chart' is a simple way of saying 'all them yaml files'. If your familier with package managers in linux (like apt or yum or dnf)helm is just that, a package manager for Kubernetes. Read the ['what-is-kubernetes'](./what-is-kubernetes.MD) for a better understand of .yaml files.

It's important to note here that:
- Helm ≠ Helm Chart ≠ Manifest, **BUT**:
    - Helm uses Helm charts as its input.
    - Helm charts generate manifests (YAML files) to apply to your cluster.

Helm is a tool used to manage super large kubernetes deployment.
