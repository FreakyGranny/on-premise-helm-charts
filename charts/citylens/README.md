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
| `api.image.tag`        | Tag.         | `1.0.5`                        |
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
| `web.image.tag`        | Tag.         | `1.0.7`                        |
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

| Name                                 | Description                                                                                                                 | Value   |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------- | ------- |
| `worker.camcomSender.enabled`        | If Camcom Sender worker is enabled for the service.                                                                         | `false` |
| `worker.camcomSender.replicas`       | A replica count for the pod.                                                                                                | `1`     |
| `worker.camcomSender.annotations`    | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`    |
| `worker.camcomSender.labels`         | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`    |
| `worker.camcomSender.podAnnotations` | Kubernetes [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/).                   | `{}`    |
| `worker.camcomSender.podLabels`      | Kubernetes [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).                             | `{}`    |
| `worker.camcomSender.nodeSelector`   | Kubernetes pod [node selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector).     | `{}`    |
| `worker.camcomSender.tolerations`    | Kubernetes pod [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) settings.       | `{}`    |
| `worker.camcomSender.affinity`       | Kubernetes pod [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) settings. | `{}`    |

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

### Migration job settings

| Name                                   | Description                                                                                                             | Value                               |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `migrations.enabled`                   | If migrations needed.                                                                                                   | `true`                              |
| `migrations.image.repository`          | Repository.                                                                                                             | `2gis-on-premise/citylens-database` |
| `migrations.image.tag`                 | Tag.                                                                                                                    | `1.0.0`                             |
| `migrations.image.pullPolicy`          | Pull Policy                                                                                                             | `IfNotPresent`                      |
| `migrations.resources.requests.cpu`    | A CPU request.                                                                                                          | `100m`                              |
| `migrations.resources.requests.memory` | A memory request.                                                                                                       | `1Gi`                               |
| `migrations.resources.limits.cpu`      | A CPU limit.                                                                                                            | `200m`                              |
| `migrations.resources.limits.memory`   | A memory limit.                                                                                                         | `2Gi`                               |
| `migrations.nodeSelector`              | Kubernetes pod [node selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector). | `{}`                                |

### Kafka settings

| Name                               | Description                                               | Value |
| ---------------------------------- | --------------------------------------------------------- | ----- |
| `kafka.bootstrapServer`            | A Kafka broker endpoint. **Required**                     | `""`  |
| `kafka.username`                   | A Kafka username for connection. **Required**             | `""`  |
| `kafka.password`                   | A Kafka password for connection. **Required**             | `""`  |
| `kafka.topics.frames`              | List of topics for Frames saver worker. **Required**      | `""`  |
| `kafka.topics.tracks`              | List of topics for Tracks metadata worker. **Required**   | `""`  |
| `kafka.topics.prediction`          | List of topics for Predictions saver worker. **Required** | `""`  |
| `kafka.topics.pro`                 | List of topics for Reporter pro worker. **Required**      | `""`  |
| `kafka.topics.camcom`              | List of topics for Camcom worker. **Required**            | `""`  |
| `kafka.topics.logs`                | List of topics for API logs. **Required**                 | `""`  |
| `kafka.topics.framesGroupId`       | Frames saver workers's group ID. **Required**             | `""`  |
| `kafka.topics.tracksGroupId`       | Tracks metadata workers's group ID. **Required**          | `""`  |
| `kafka.topics.predictionGroupId`   | Predictions saver workers's group ID. **Required**        | `""`  |
| `kafka.topics.camcomSenderGroupId` | Camcom saver workers's group ID. **Required**             | `""`  |

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

### Custom settings

| Name              | Description                                | Value                  |
| ----------------- | ------------------------------------------ | ---------------------- |
| `dashboardDomain` | Link to Citylens web address. **Required** | `""`                   |
| `locale`          | Locale language (en by default).           | `en`                   |
| `headerLinks`     | List of links.                             | `["drivers","tracks"]` |
| `reporters`       | List of reporters.                         | `["pro"]`              |
| `predictors`      | List of predictors.                        | `["camcom"]`           |