# Agent Guide

## Generic Chart (`charts/generic`)

A reusable Helm chart for running any Docker image that doesn't have an official chart. Uses the `common` library chart (`charts/common`) as a dependency.

### Usage

Create a `values.yaml` with your app config:

```yaml
image:
  repository: my-app
  tag: latest
ports:
  - name: http
    containerPort: 3000
service:
  ports:
    - port: 3000
      targetPort: http
```

Then install:

```bash
helm install my-release charts/generic -f my-values.yaml
```

### Key Features

- **Deployment** with full container config: image, env, probes, resources, volumes, init containers, scheduling
- **Service** with configurable type and ports
- **Ingress** with TLS, annotations, className
- **ConfigMap/Secret** from values
- **ServiceAccount** with annotations and imagePullSecrets
- **PersistentVolumeClaim** with automatic pod mount
- **HPA** with CPU/memory target utilization
- All resources are optional (disabled by default)

### Values

See `charts/generic/values.yaml` for the full schema.

## Common Library Chart (`charts/common`)

Library chart providing reusable templates for: Deployment, Service, ConfigMap, Secret, ServiceAccount, ClusterRole, ClusterRoleBinding.

Dependent charts use the merge pattern:

```yaml
{{- include "common.deployment" (list . "mychart.deployment") }}
{{- define "mychart.deployment" }}
spec:
  template:
    spec:
      containers:
        - name: myapp
          image: myapp:latest
{{- end }}
```

## CI/CD

- **Release workflow** (`.github/workflows/publish_chart.yaml`): On merge to `main`, `helm/chart-releaser-action` packages changed charts (with `helm dependency update` first) and publishes them as GitHub Releases with a `gh-pages` index.
- **Renovate** (`.github/renovate-config.js`): Runs every 2 hours, manages Helm chart dependencies and bumps chart versions as `patch` updates.
- To trigger a release: increment `version` in `Chart.yaml`, merge to `main`.
