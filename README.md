# Helm Chart for swagger
<!--
[![CircleCI](https://circleci.com/gh/cetic/helm-swagger.svg?style=svg)](https://circleci.com/gh/cetic/helm-swagger/tree/master) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) ![version](https://img.shields.io/github/tag/cetic/helm-swagger.svg?label=release)

## Introduction

This [Helm](https://github.com/kubernetes/helm) chart installs [swagger](https://github.com/postgres/swagger4) in a Kubernetes cluster.

## Prerequisites

- Kubernetes cluster 1.10+
- Helm 2.8.0+
- PV provisioner support in the underlying infrastructure.

## Installation

### Add Helm repository

```bash
helm repo add cetic https://cetic.github.io/helm-charts
helm repo update
```

### Configure the chart

The following items can be set via `--set` flag during installation or configured by editing the `values.yaml` directly (need to download the chart first).

#### Configure the way how to expose swagger service:

- **Ingress**: The ingress controller must be installed in the Kubernetes cluster.
- **ClusterIP**: Exposes the service on a cluster-internal IP. Choosing this value makes the service only reachable from within the cluster.
- **NodePort**: Exposes the service on each Node’s IP at a static port (the NodePort). You’ll be able to contact the NodePort service, from outside the cluster, by requesting `NodeIP:NodePort`.
- **LoadBalancer**: Exposes the service externally using a cloud provider’s load balancer.

#### Configure the way how to persistent data:

- **Disable**: The data does not survive the termination of a pod.
- **Persistent Volume Claim(default)**: A default `StorageClass` is needed in the Kubernetes cluster to dynamic provision the volumes. Specify another StorageClass in the `storageClass` or set `existingClaim` if you have already existing persistent volumes to use.

### Install the chart

Install the swagger helm chart with a release name `my-release`:

```bash
helm install --name my-release cetic/swagger
```

## Uninstallation

To uninstall/delete the `my-release` deployment:

```bash
helm delete --purge my-release
```

## Configuration

The following table lists the configurable parameters of the swagger chart and the default values.

| Parameter                                                                   | Description                                                                                                        | Default                         |
| --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------| ------------------------------- |
| **Image**                                                                   |
| `image.repository`                                                          | swagger Image name                                                                                                 | `dpage/swagger4`                |
| `image.tag`                                                                 | swagger Image tag                                                                                                  | `4.11`                          |
| `image.pullPolicy`                                                          | swagger Image pull policy                                                                                          | `IfNotPresent`                  |
| **swagger**                                                                 |
| `swagger.username`                                                          | swagger admin user                                                                                                 | `swagger4@swagger.org`          |
| `swagger.password`                                                          | swagger admin password                                                                                             | `admin`                         |
| `swagger.tls`                                                               | swagger admin TLS. the container will listen on port 80 for connections in plain text. If set to any value, the container will listen on port 443 for TLS connections. When TLS is enabled, a certificate and key must be provided. See [secrets file](/templates/secrets.yaml)| `false`                         |
| `swagger.scriptname`                                                        | swagger ScriptName Env, See https://www.swagger.org/docs/swagger4/latest/container_deployment.html                 | `nil`                         |
| **Persistence**                                                             |
| `persistence.enabled`                                                       | Enable the data persistence or not                                                                                 | `true`                          |
| `persistence.existingClaim`                                                 | Provide an existing PersistentVolumeClaim, the value is evaluated as a template                                    | `nil`                           |
| `persistence.storageClass`                                                  | PVC Storage Class for PostgreSQL volume                                                                            | `nil`                           |
| `persistence.accessMode`                                                    | The access mode of the volume                                                                                      | `ReadWriteOnce`                 |
| `persistence.size`                                                          | The size of the volume                                                                                             | `4Gi`                           |
| **Service**                                                                 |
| `service.type`                                                              | Type of service for swagger frontend                                                                               | `LoadBalancer`                  |
| `service.port`                                                              | Port to expose service                                                                                             | `80`                            |
| `service.tlsport`                                                           | Port to expose service in tls, `swagger.tls`must be enabled                                                        | `443`                           |
| `service.loadBalancerIP`                                                    | LoadBalancerIP if service type is `LoadBalancer`                                                                   | `nil`                           |
| `service.loadBalancerSourceRanges`                                          | Address that are allowed when svc is `LoadBalancer`                                                                | `[]`                            |
| `service.annotations`                                                       | Service annotations                                                                                                | `{}`                            |
| **Ingress**                                                                 |
| `ingress.enabled`                                                           | Enables Ingress                                                                                                    | `false`                         |
| `ingress.annotations`                                                       | Ingress annotations                                                                                                | `{}`                            |
| `ingress.path`                                                              | Path to access frontend                                                                                            | `/`                             |
| `ingress.hosts`                                                             | Ingress hosts                                                                                                      | `[]`                            |
| `ingress.tls`                                                               | Ingress TLS configuration                                                                                          | `[]`                            |
| **Servers**                                                                 |
| `servers.enabled`                                                           | Enable the servers configuration. If enabled, server definitions found in `servers.config` will be loaded at launch time.| `true`                    |
| `servers.config`                                                            | Server definitions                                                                                                 | `See the values.yaml`           |
| **ReadinessProbe**                                                          |
| `readinessProbe`                                                            | Rediness Probe settings                                                                                            | `nil`                           |
| **LivenessProbe**                                                           |
| `livenessProbe`                                                             | Liveness Probe settings                                                                                            | `nil`                           |
| **Resources**                                                               |
| `resources`                                                                 | CPU/Memory resource requests/limits                                                                                | `{}`                            |

## Credits

Initially inspired from https://github.com/jjcollinge/swagger-chart, which is archived.

## Contributing

Feel free to contribute by making a [pull request](https://github.com/cetic/helm-swagger/pull/new/master).

Please read the official [Contribution Guide](https://github.com/helm/charts/blob/master/CONTRIBUTING.md) from Helm for more information on how you can contribute to this Chart.

## License

[Apache License 2.0](/LICENSE.md) -->
