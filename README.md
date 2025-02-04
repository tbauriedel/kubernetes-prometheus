# Kubernetes Cluster Setup

This repository contains the configuration files and installation guides for setting up various components in a Kubernetes cluster. The components include cert-manager, ingress-nginx, longhorn, and a monitoring stack with Prometheus, Grafana, and node-exporter.

## Folder Structure

### Certificates
- `cert-manager/`
  - `01-Installation.md`: Instructions for installing cert-manager using Helm.
  - `02-ClusterIssuer.yml`: YAML configuration for creating a self-signed ClusterIssuer.

### Ingress
- `ingress-nginx/`
  - `01-Installation.md`: Instructions for installing ingress-nginx using Helm.

### Volumes
- `longhorn/`
  - `01-Installation.md`: Instructions for installing Longhorn using Helm.
  - `02-Certificates.yml`: YAML configuration for creating a TLS certificate for Longhorn.
  - `03-Ingress.yml`: YAML configuration for setting up an Ingress for Longhorn with basic authentication.

### Prometheus
- `monitoring-stack/`
  - `Namespace.yml`: YAML configuration for creating the `monitoring` namespace.
  - `generate_encrypted_pass.py`: Python script for generating encrypted passwords using bcrypt.
  - `grafana/`
    - `01-Certificates.yml`: YAML configuration for creating a TLS certificate for Grafana.
    - `02-PVC.yml`: YAML configuration for creating a PersistentVolumeClaim for Grafana data.
    - `03-ConfigMaps.yml`: YAML configuration for creating a ConfigMap for Grafana settings.
    - `04-Deployment.yml`: YAML configuration for deploying Grafana.
    - `05-Service.yml`: YAML configuration for creating a Service for Grafana.
    - `06-Ingress.yml`: YAML configuration for setting up an Ingress for Grafana.
  - `exporter/`
    - `node_exporter/`
      - `01-Certificates.yml`: YAML configuration for creating a TLS certificate for node-exporter.
      - `02-ConfigMaps.yml`: YAML configuration for creating a ConfigMap for node-exporter settings.
      - `03-DaemonSet.yml`: YAML configuration for deploying node-exporter as a DaemonSet.
      - `04-Service.yml`: YAML configuration for creating a Service for node-exporter.
  - `prometheus/`
    - `01-ClusterRole.yml`: YAML configuration for creating a ClusterRole for Prometheus node discovery.
    - `02-ServiceAccount.yml`: YAML configuration for creating a ServiceAccount for Prometheus.
    - `03-ClusterRoleBinding.yml`: YAML configuration for binding the ClusterRole to the ServiceAccount.
    - `04-Certificates.yml`: YAML configuration for creating a TLS certificate for Prometheus.
    - `05-PVC.yml`: YAML configuration for creating a PersistentVolumeClaim for Prometheus data.
    - `06-ConfigMaps.yml`: YAML configuration for creating ConfigMaps for Prometheus settings.
    - `07-Deployment.yml`: YAML configuration for deploying Prometheus.
    - `08-Service.yml`: YAML configuration for creating a Service for Prometheus.

### Generating Encrypted Passwords

Use the `generate_encrypted_pass.py` script in the `monitoring-stack/` folder to generate encrypted passwords for basic authentication.

```sh
python monitoring-stack/generate_encrypted_pass.py
```