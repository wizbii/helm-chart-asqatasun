# Asqatasun

[Asqatasun](https://asqatasun.org/) is an opensource website analyzer, used for web accessibility (a11y).

## Introduction

This chart bootstraps an instance of Asqatasun, on version 5.0.0-rc.1, with a MySQL 5.7 database.
To install a different version, refer to the values.yaml file.

For more details about the version to use, see : https://gitlab.com/asqatasun/asqatasun-docker

:warning: This chart use a Docker image not ready for production yet, with no security features. 

## Requirements

| Repository                         | Name  | Version |
|------------------------------------|-------|---------|
| https://charts.bitnami.com/bitnami | mysql | ~9.18   |

## Configuration

### Global

| Key              | Type   | Default | Description                                 |
|------------------|--------|---------|---------------------------------------------|
| annotations      | object | `{}`    | Pod annotations                             |
| env              | list   | `[]`    | Environment variables to attach to the pods |
| fullnameOverride | string | `""`    |                                             |
| nameOverride     | string | `""`    |                                             |
| podLabels        | object | `{}`    | Map of labels to add to the pods            |
| replicaCount     | int    | `1`     | Number of replicas deployed                 |

### Extra configs

extraConfig is used to load Environment Variables from Secrets and ConfigMaps

| Key                    | Type | Default | Description                                                                                                             |
|------------------------|------|---------|-------------------------------------------------------------------------------------------------------------------------|
| extraConfig.configmaps | list | `[]`    | A list of Secrets (which must contain key/value pairs) which may be loaded into the container as environment variables	 |
| extraConfig.secrets    | list | `[]`    | A list of Secrets (which must contain key/value pairs) which may be loaded into the container as environment variables  |

### Image

| Key              | Type   | Default                 | Description                                                    |
|------------------|--------|-------------------------|----------------------------------------------------------------|
| image.pullPolicy | string | `"IfNotPresent"`        | Image pull policy                                              |
| image.repository | string | `"asqatasun/asqatasun"` | Image repository                                               |
| image.tag        | string | `"5.0.0-rc.1"`          | Overrides the image tag whose default is the chart appVersion. |

### Ingress

| Key                   | Type   | Default                    | Description                                   |
|-----------------------|--------|----------------------------|-----------------------------------------------|
| ingress.annotations   | object | `{}`                       | Field to add extra annotations to the ingress |
| ingress.enabled       | bool   | `false`                    | Flag to enable Ingress                        |
| ingress.hosts[0].name | string | `"asqatasun.your-org.com"` | Hostname to your Asqatasun installation       |
| ingress.hosts[0].path | string | `"/"`                      | Path within the URL structure                 |
| ingress.tls           | list   | `[]`                       | Ingress secrets for TLS certificates          |

### JDBC

Database configuration. 
If you use the bundled database (i.e. `mysql.enabled: true`), configure these values to match the bundled configuration

| Key                    | Type   | Default                           | Description                                                                                    |
|------------------------|--------|-----------------------------------|------------------------------------------------------------------------------------------------|
| jdbc.database          | string | `"asqatasun"`                     | Database name                                                                                  |
| jdbc.driver            | string | `"mysql"`                         | JDBC driver                                                                                    |
| jdbc.host              | string | `"asqatasun-db"`                  | JDBC Host                                                                                      |
| jdbc.password          | string | `"asqatasunDatabaseUserP4ssword"` | Use this if you don't mind the DB password getting stored in plain text within the values file |
| jdbc.port              | string | `"3306"`                          | JDBC Port                                                                                      |
| jdbc.secretName        | string | `""`                              | Secret name for database password                                                              |
| jdbc.secretPasswordKey | string | `""`                              | Secret key for database password                                                               |
| jdbc.username          | string | `"asqatasunDatabaseUserLogin"`    | Database username                                                                              |

### Probes

| Key                                | Type   | Default | Description                                    |
|------------------------------------|--------|---------|------------------------------------------------|
| livenessProbe.failureThreshold     | int    | `2`     | LivenessProbe threshold for marking as dead    |
| livenessProbe.initialDelaySeconds  | int    | `15`    | LivenessProbe initial delay for checks         |
| livenessProbe.path                 | string | `"/"`   | Path for the HTTP probe                        |
| livenessProbe.periodSeconds        | int    | `10`    | LivenessProbe period between checks            |
| livenessProbe.timeoutSeconds       | int    | `1`     | LivenessProbe timeout delay                    |
| readinessProbe.failureThreshold    | int    | `2`     | ReadinessProbe threshold for marking as failed |
| readinessProbe.initialDelaySeconds | int    | `15`    | ReadinessProbe initial delay for checks        |
| readinessProbe.path                | string | `"/"`   | Path for the HTTP probe                        |
| readinessProbe.periodSeconds       | int    | `10`    | ReadinessProbe period between checks           |
| readinessProbe.timeoutSeconds      | int    | `1`     | ReadinessProbe timeout delay                   |

### MySQL

Configuration for MySQL dependency. See [this doc](https://github.com/bitnami/charts/blob/main/bitnami/mysql/README.md) for all configuration variables.

| Key                 | Type   | Default                           | Description                         |
|---------------------|--------|-----------------------------------|-------------------------------------|
| mysql.enabled       | bool   | `true`                            | Set to false to use external server |
| mysql.auth.database | string | `"asqatasun"`                     | MySQL database name                 |
| mysql.auth.password | string | `"asqatasunDatabaseUserP4ssword"` | MySQL database password             |
| mysql.auth.username | string | `"asqatasunDatabaseUserLogin"`    | MySQL database user                 |
| mysql.image.tag     | string | `"5.7"`                           | MySQL image tag to use              |

### Resources

Adjust these values to your needs, but make sure that the memory limit is never under 4 GB

| Key                       | Type   | Default | Description              |
|---------------------------|--------|---------|--------------------------|
| resources.limits.cpu      | int    | `2`     | Asqatasun CPU Asqatasun  |
| resources.limits.memory   | string | `"4Gi"` | Asqatasun memory limits  |
| resources.requests.cpu    | int    | `1`     | Asqatasun CPU request    |
| resources.requests.memory | string | `"2Gi"` | Asqatasun memory request |

### Service

| Key                  | Type   | Default       | Description               |
|----------------------|--------|---------------|---------------------------|
| service.externalPort | int    | `80`          | Kubernetes service port   |
| service.internalPort | int    | `8080`        | Kubernetes container port |
| service.type         | string | `"ClusterIP"` | Kubernetes service type   |

### Service Account

| Key                        | Type   | Default | Description                                                                                                            |
|----------------------------|--------|---------|------------------------------------------------------------------------------------------------------------------------|
| serviceAccount.annotations | object | `{}`    | Annotations to add to the service account                                                                              |
| serviceAccount.create      | bool   | `false` | Specifies whether a service account should be created                                                                  |
| serviceAccount.name        | string | `""`    | The name of the service account to use. If not set and create is true, a name is generated using the fullname template |
