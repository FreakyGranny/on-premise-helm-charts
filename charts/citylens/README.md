# 2GIS Citylens service

Use this Helm chart to deploy Citylens services, which is a part of 2GIS's [On-Premise recognitions services]().

Read more about the On-Premise solution [here](https://docs.2gis.com/en/on-premise/overview).

> **Note:**
>
> All On-Premise services are beta, and under development.

See the [documentation]() to learn about:

- Architecture of the service.

- Installing the service.

    When filling in the keys for `values.yaml` configuration file, refer to the documentation and the list of keys below.

- Updating the service.

## Values

### Docker Registry settings

| Name                  | Description                                                                                         | Value |
| --------------------- | --------------------------------------------------------------------------------------------------- | ----- |
| `dgctlDockerRegistry` | Docker Registry endpoint where On-Premise services' images reside. Format: `host:port` **Required** | `""`  |

### Citylens API service settings


### Image settings

| Name                   | Description  | Value                          |
| ---------------------- | ------------ | ------------------------------ |
| `api.image.repository` | Repository.  | `2gis-on-premise/citylens-api` |
| `api.image.tag`        | Tag.         | `1.0.9`                        |
| `api.image.pullPolicy` | Pull Policy. | `IfNotPresent`                 |

### Resources settings

| Name                            | Description                  | Value   |
| ------------------------------- | ---------------------------- | ------- |
| `api.replicas`                  | A replica count for the pod. | `4`     |
| `api.resources.requests.cpu`    | A CPU request.               | `1000m` |
| `api.resources.requests.memory` | A memory request.            | `1Gi`   |
| `api.resources.limits.cpu`      | A CPU limit.                 | `2000m` |
| `api.resources.limits.memory`   | A memory limit.              | `2Gi`   |

### Service settings

| Name                      | Description                                                                                                                    | Value       |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ----------- |
| `api.service.type`        | Kubernetes [service type](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types). | `ClusterIP` |
| `api.service.port`        | Service port.                                                                                                                  | `80`        |
| `api.service.targetPort`  | Service target port.                                                                                                           | `8000`      |
| `api.service.annotations` | Kubernetes [service annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).              | `{}`        |
| `api.service.labels`      | Kubernetes [service labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                        | `{}`        |

### Kubernetes [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) settings

| Name                                                                  | Description                                                                                                           | Value                                                 |
| --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| `api.ingress.enabled`                                                 | If Ingress is enabled for the service.                                                                                | `true`                                                |
| `api.ingress.className`                                               | Resource that contains additional configuration including the name of the controller that should implement the class. | `""`                                                  |
| `api.ingress.annotations.nginx.ingress.kubernetes.io/proxy-body-size` | Proxy-body-size parameter (default 1MB).                                                                              | `{"nginx.ingress.kubernetes.io/proxy-body-size":"0"}` |
| `api.ingress.hosts[0].host`                                           | Hostname for the Ingress service. Ex.: 'citylens.api'.                                                                | `citylens.host`                                       |
| `api.ingress.hosts[0].paths[0].path`                                  | Endpoint of host.                                                                                                     | `/`                                                   |
| `api.ingress.hosts[0].paths[0].pathType`                              | Path type of endpoint.                                                                                                | `Prefix`                                              |
| `api.ingress.tls`                                                     | Tls settings for https.                                                                                               | `[]`                                                  |

### Auth settings for authentication

| Name                 | Description                                                                                                         | Value   |
| -------------------- | ------------------------------------------------------------------------------------------------------------------- | ------- |
| `api.auth.enabled`   | If authentication is needed.                                                                                        | `true`  |
| `api.auth.publicKey` | Public Key for authentication. Visit `http(s)://keycloak.ingress.host/realms/CityLens_app/` to obtain a Public Key. | `""`    |
| `api.auth.algorithm` | Authentication algorithm type.                                                                                      | `RS256` |

### Custom settings

| Name           | Description                        | Value   |
| -------------- | ---------------------------------- | ------- |
| `api.showDocs` | Show documentation link if needed. | `false` |
| `api.logLevel` | Log level.                         | `INFO`  |

### Metadata settings

| Name                 | Description                                                                                                                 | Value |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------- | ----- |
| `api.annotations`    | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `api.labels`         | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `api.podAnnotations` | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `api.podLabels`      | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `api.nodeSelector`   | Kubernetes pod [node selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector).     | `{}`  |
| `api.tolerations`    | Kubernetes pod [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) settings.       | `{}`  |
| `api.affinity`       | Kubernetes pod [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) settings. | `{}`  |

### Citylens web service settings


### Image settings

| Name                   | Description  | Value                          |
| ---------------------- | ------------ | ------------------------------ |
| `web.image.repository` | Repository.  | `2gis-on-premise/citylens-web` |
| `web.image.tag`        | Tag.         | `1.0.13`                       |
| `web.image.pullPolicy` | Pull Policy. | `IfNotPresent`                 |

### Resources settings

| Name                            | Description                  | Value   |
| ------------------------------- | ---------------------------- | ------- |
| `web.replicas`                  | A replica count for the pod. | `1`     |
| `web.resources.requests.cpu`    | A CPU request.               | `1000m` |
| `web.resources.requests.memory` | A memory request.            | `1Gi`   |
| `web.resources.limits.cpu`      | A CPU limit.                 | `2000m` |
| `web.resources.limits.memory`   | A memory limit.              | `2Gi`   |

### Service settings

| Name                      | Description                                                                                                                    | Value       |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ----------- |
| `web.service.type`        | Kubernetes [service type](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types). | `ClusterIP` |
| `web.service.port`        | Service port.                                                                                                                  | `80`        |
| `web.service.targetPort`  | Service target port.                                                                                                           | `5000`      |
| `web.service.annotations` | Kubernetes [service annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).              | `{}`        |
| `web.service.labels`      | Kubernetes [service labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                        | `{}`        |

### Kubernetes [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) settings

| Name                                                                  | Description                                                                                                           | Value                                                 |
| --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| `web.ingress.enabled`                                                 | If Ingress is enabled for the service.                                                                                | `true`                                                |
| `web.ingress.className`                                               | Resource that contains additional configuration including the name of the controller that should implement the class. | `""`                                                  |
| `web.ingress.annotations.nginx.ingress.kubernetes.io/proxy-body-size` | Proxy-body-size parameter (default 1MB).                                                                              | `{"nginx.ingress.kubernetes.io/proxy-body-size":"0"}` |
| `web.ingress.hosts[0].host`                                           | Hostname for the Ingress service. Ex.: 'citylens.web'.                                                                | `citylens.host`                                       |
| `web.ingress.hosts[0].paths[0].path`                                  | Endpoint of host.                                                                                                     | `/`                                                   |
| `web.ingress.hosts[0].paths[0].pathType`                              | Path type of endpoint.                                                                                                | `Prefix`                                              |
| `web.ingress.tls`                                                     | Tls settings for https.                                                                                               | `[]`                                                  |

### Auth settings for authentication

| Name                     | Description                                                                                | Value   |
| ------------------------ | ------------------------------------------------------------------------------------------ | ------- |
| `web.auth.enabled`       | If authentication is needed.                                                               | `false` |
| `web.auth.realm`         | Authenitcation realm, example: Inspection_Portal_backend **Required**                      | `""`    |
| `web.auth.authServerUrl` | API URL of authentication service. Example: `http(s)://keycloak.ingress.host` **Required** | `""`    |
| `web.auth.clientId`      | Client id from keycloak, example: citylens-web-client **Required**                         | `""`    |
| `web.auth.clientSecret`  | Client Secret from keycloak. **Required**                                                  | `""`    |
| `web.auth.verifySsl`     | Enable\Disable SSL check.                                                                  | `true`  |

### Custom settings

| Name           | Description | Value     |
| -------------- | ----------- | --------- |
| `web.logLevel` | Log level.  | `WARNING` |

### Metadata settings

| Name                 | Description                                                                                                                 | Value |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------- | ----- |
| `web.annotations`    | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `web.labels`         | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `web.podAnnotations` | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `web.podLabels`      | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `web.nodeSelector`   | Kubernetes pod [node selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector).     | `{}`  |
| `web.tolerations`    | Kubernetes pod [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) settings.       | `{}`  |
| `web.affinity`       | Kubernetes pod [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) settings. | `{}`  |

### Citylens workers service settings


### Resources settings

| Name                               | Description       | Value   |
| ---------------------------------- | ----------------- | ------- |
| `worker.resources.requests.cpu`    | A CPU request.    | `1000m` |
| `worker.resources.requests.memory` | A memory request. | `1Gi`   |
| `worker.resources.limits.cpu`      | A CPU limit.      | `2000m` |
| `worker.resources.limits.memory`   | A memory limit.   | `2Gi`   |

### Citylens Frames Saver worker's settings

| Name                                | Description                                                                                                                 | Value |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ----- |
| `worker.framesSaver.replicas`       | A replica count for the pod.                                                                                                | `4`   |
| `worker.framesSaver.annotations`    | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `worker.framesSaver.labels`         | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `worker.framesSaver.podAnnotations` | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `worker.framesSaver.podLabels`      | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `worker.framesSaver.nodeSelector`   | Kubernetes pod [node selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector).     | `{}`  |
| `worker.framesSaver.tolerations`    | Kubernetes pod [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) settings.       | `{}`  |
| `worker.framesSaver.affinity`       | Kubernetes pod [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) settings. | `{}`  |

### Citylens Camcom sender worker's settings

| Name                                          | Description                                                                                                                 | Value   |
| --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ------- |
| `worker.camcomSender.enabled`                 | If Camcom Sender worker is enabled for the service.                                                                         | `false` |
| `worker.camcomSender.replicas`                | A replica count for the pod.                                                                                                | `1`     |
| `worker.camcomSender.apiKey`                  | A key for Camcom's API access                                                                                               | `""`    |
| `worker.camcomSender.endpointUrl`             | Camcom endpoint URL                                                                                                         | `""`    |
| `worker.camcomSender.requestTimeout`          | Camcom request timeout                                                                                                      | `1`     |
| `worker.camcomSender.requestRateLimit.calls`  | Camcom calls rate limit                                                                                                     | `1000`  |
| `worker.camcomSender.requestRateLimit.period` | Camcom period rate limit                                                                                                    | `60`    |
| `worker.camcomSender.requestRetries`          | Camcom request retries                                                                                                      | `3`     |
| `worker.camcomSender.requestRetriesBackoff`   | request retries backoff                                                                                                     | `1`     |
| `worker.camcomSender.annotations`             | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`    |
| `worker.camcomSender.labels`                  | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`    |
| `worker.camcomSender.podAnnotations`          | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`    |
| `worker.camcomSender.podLabels`               | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`    |
| `worker.camcomSender.nodeSelector`            | Kubernetes pod [node selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector).     | `{}`    |
| `worker.camcomSender.tolerations`             | Kubernetes pod [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) settings.       | `{}`    |
| `worker.camcomSender.affinity`                | Kubernetes pod [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) settings. | `{}`    |

### Citylens Predictions Saver worker's settings

| Name                                     | Description                                                                                                                 | Value |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ----- |
| `worker.predictionsSaver.replicas`       | A replica count for the pod.                                                                                                | `1`   |
| `worker.predictionsSaver.annotations`    | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `worker.predictionsSaver.labels`         | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `worker.predictionsSaver.podAnnotations` | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `worker.predictionsSaver.podLabels`      | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `worker.predictionsSaver.nodeSelector`   | Kubernetes pod [node selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector).     | `{}`  |
| `worker.predictionsSaver.tolerations`    | Kubernetes pod [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) settings.       | `{}`  |
| `worker.predictionsSaver.affinity`       | Kubernetes pod [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) settings. | `{}`  |

### Citylens Reporter Pro worker's settings

| Name                                | Description                                                                                                                 | Value |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ----- |
| `worker.reporterPro.replicas`       | A replica count for the pod.                                                                                                | `1`   |
| `worker.reporterPro.annotations`    | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `worker.reporterPro.labels`         | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `worker.reporterPro.podAnnotations` | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `worker.reporterPro.podLabels`      | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `worker.reporterPro.nodeSelector`   | Kubernetes pod [node selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector).     | `{}`  |
| `worker.reporterPro.tolerations`    | Kubernetes pod [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) settings.       | `{}`  |
| `worker.reporterPro.affinity`       | Kubernetes pod [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) settings. | `{}`  |

### Citylens Track Metadata Saver worker's settings

| Name                                       | Description                                                                                                                 | Value |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------- | ----- |
| `worker.trackMetadataSaver.replicas`       | A replica count for the pod.                                                                                                | `1`   |
| `worker.trackMetadataSaver.annotations`    | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `worker.trackMetadataSaver.labels`         | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `worker.trackMetadataSaver.podAnnotations` | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`  |
| `worker.trackMetadataSaver.podLabels`      | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`  |
| `worker.trackMetadataSaver.nodeSelector`   | Kubernetes pod [node selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector).     | `{}`  |
| `worker.trackMetadataSaver.tolerations`    | Kubernetes pod [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) settings.       | `{}`  |
| `worker.trackMetadataSaver.affinity`       | Kubernetes pod [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) settings. | `{}`  |

### Citylens Tracks Uploader worker's settings

| Name                                   | Description                                                                                                                 | Value  |
| -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ------ |
| `worker.tracksUploader.enabled`        | If Tracks Uploader worker is enabled for the service.                                                                       | `true` |
| `worker.tracksUploader.replicas`       | A replica count for the pod.                                                                                                | `1`    |
| `worker.tracksUploader.api`            | API address.                                                                                                                | `""`   |
| `worker.tracksUploader.source`         | Source.                                                                                                                     | `""`   |
| `worker.tracksUploader.annotations`    | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`   |
| `worker.tracksUploader.labels`         | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`   |
| `worker.tracksUploader.podAnnotations` | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`   |
| `worker.tracksUploader.podLabels`      | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`   |
| `worker.tracksUploader.nodeSelector`   | Kubernetes pod [node selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector).     | `{}`   |
| `worker.tracksUploader.tolerations`    | Kubernetes pod [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) settings.       | `{}`   |
| `worker.tracksUploader.affinity`       | Kubernetes pod [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) settings. | `{}`   |

### Migration job settings

| Name                                   | Description                                                                                                             | Value                               |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `migrations.enabled`                   | If migrations needed.                                                                                                   | `true`                              |
| `migrations.image.repository`          | Repository.                                                                                                             | `2gis-on-premise/citylens-database` |
| `migrations.image.tag`                 | Tag.                                                                                                                    | `1.0.9`                             |
| `migrations.image.pullPolicy`          | Pull Policy                                                                                                             | `IfNotPresent`                      |
| `migrations.resources.requests.cpu`    | A CPU request.                                                                                                          | `100m`                              |
| `migrations.resources.requests.memory` | A memory request.                                                                                                       | `1Gi`                               |
| `migrations.resources.limits.cpu`      | A CPU limit.                                                                                                            | `200m`                              |
| `migrations.resources.limits.memory`   | A memory limit.                                                                                                         | `2Gi`                               |
| `migrations.nodeSelector`              | Kubernetes pod [node selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector). | `{}`                                |

### Kafka settings

| Name                          | Description                                              | Value    |
| ----------------------------- | -------------------------------------------------------- | -------- |
| `kafka.bootstrapServer`       | A Kafka broker endpoint. **Required**                    | `""`     |
| `kafka.username`              | A Kafka username for connection. **Required**            | `""`     |
| `kafka.password`              | A Kafka password for connection. **Required**            | `""`     |
| `kafka.topics.frames`         | List of topics for Frames saver worker. **Required**     | `""`     |
| `kafka.topics.tracks`         | List of topics for Tracks metadata worker. **Required**2 | `""`     |
| `kafka.topics.pro`            | List of topics for Reporter pro worker. **Required**     | `""`     |
| `kafka.topics.camcom`         | List of topics for Camcom worker. **Required**           | `""`     |
| `kafka.topics.uploader`       | List of topics for Uploader worker. **Required**         | `""`     |
| `kafka.topics.logs`           | List of topics for API logs. **Required**                | `""`     |
| `kafka.consumerGroups.prefix` | Kafka topics prefix. **Required**                        | `""`     |
| `kafka.predictors[0].name`    | Name of predictor **Required**                           | `camcom` |
| `kafka.predictors[0].topic`   | Topic used by predictor **Required**                     | `""`     |

### S3 settings

| Name                 | Description                                             | Value |
| -------------------- | ------------------------------------------------------- | ----- |
| `s3.endpoint`        | S3 endpoint. Format: `host:port` or `url`. **Required** | `""`  |
| `s3.accessKey`       | S3 access key for accessing the bucket. **Required**    | `""`  |
| `s3.secretAccessKey` | S3 secret key for accessing the bucket. **Required**    | `""`  |
| `s3.bucketPrefix`    | S3 bucket name. **Required**                            | `""`  |

### postgres **Database settings**

| Name                | Description                                      | Value  |
| ------------------- | ------------------------------------------------ | ------ |
| `postgres.host`     | PostgreSQL rw hostname or IP. **Required**       | `""`   |
| `postgres.port`     | PostgreSQL port. **Required**                    | `5432` |
| `postgres.database` | PostgreSQL database name. **Required**           | `""`   |
| `postgres.username` | PostgreSQL username with rw access. **Required** | `""`   |
| `postgres.password` | PostgreSQL password. **Required**                | `""`   |

### Map settings

| Name                     | Description                            | Value |
| ------------------------ | -------------------------------------- | ----- |
| `map.mapgl.host`         | Hostname of mapgl server. **Required** | `""`  |
| `map.mapgl.key`          | Key of mapgl server. **Required**      | `""`  |
| `map.projects[0].name`   | Name of project.                       | `""`  |
| `map.projects[0].coords` | Coordinates of area.                   | `[]`  |
| `map.initialProject`     | Default project shown on Map.          | `""`  |

### Custom settings

| Name                      | Description                                | Value                        |
| ------------------------- | ------------------------------------------ | ---------------------------- |
| `dashboardDomain`         | Link to Citylens web address. **Required** | `""`                         |
| `locale`                  | Locale language (en by default).           | `en`                         |
| `headerLinks`             | List of links.                             | `["drivers","tracks","map"]` |
| `reporters[0].name`       | Reporter name.                             | `pro`                        |
| `reporters[0].predictors` | Predictor used by reporter.                | `["camcom"]`                 |
