# Spring Chart

[Spring](http://spring.io/) is a modern Java framework.

## Chart Details

This chart is designed to be a general purpose chart for running Spring based applications.

**Release name must be suffix by `-stable` or `-canary`**

## Add repo

To add repo with the name `stephane80000`:

```bash
$ helm repo add stephane80000 https://stephane80000.github.io/helm-charts/
$ helm repo update
```

## Installing the Chart

To install the chart with the release name `myapp-stable` and YAML files that specifies the values for the parameters `values-xxx.yaml` and secrets `values-secret-xxx.yaml` in the namespace `mynamespace` :

```bash
$ helm install myapp-stable stephane80000/spring --version X.X.X -n mynamespace -f values-xxx.yaml -f values-secret-xxx.yaml --set image.repository=de.icr.io/myimage,image.tag=0.0.2
```

## Upgrade release

To install the chart with the release name `myapp-stable` and a YAML file that specifies the values for the parameters `values-xxx.yaml` and secrets `values-secret-xxx.yaml` in the namespace `mynamespace` :

```bash
$ helm upgrade myapp-stable stephane80000/spring --version X.X.X -n mynamespace -f values-xxx.yaml -f values-secret-xxx.yaml --reuse-values
```

## Uninstalling the Chart

To uninstall/delete the `myapp-stable` deployment:

```console
helm uninstall myapp-stable
```

The command removes nearly all the Kubernetes components associated with the
chart and deletes the release.

## Configuration

The following table lists the configurable parameters and their default values.

Alternatively, you can sepcify each parameter using the `--set key=value[,key=value]` argument to `helm install`.


> **Tip**: You can donwload the sample [spring/values.yaml](spring/values.yaml)

| Parameter | Description | Default |
|-----------|-------------|---------|
| `codeapp` | The application code | `00000` |
| `tier` |  | `PA` |
| `function` |  | `nil` |
| `version` |  | `stable` |
| `javaopts` |  | `-Dspring.profiles.active=cloud-dev -Dspring.config.additional-location=/applis/config/external-config.yml` |
| `resources.limits.cpu` | Resource requests and limits | `1000m` |
| `resources.limits.memory` | Resource requests and limits | `512Mi` |
| `resources.requests.cpu` | Resource requests and limits | `100m` |
| `resources.requests.memory` | Resource requests and limits | `256Mi` |
| `spring.config.content` | YAML to be placed in `/config/application.yml` | `nil` |
| `clientCerts.enabled` | Load client certificate from secret `<myrelease>-security` in /applis/security | `false` | 
| `replicaCount` | The number of replicas | `1` |
| `service.enabled` | Enable creating a service | `true` |
| `service.type` | Kubernetes Service type | `ClusterIP` |
| `service.httpPort`| Service HTTP port | `80` |
| `ingress.enabled` | Enable ingress controller resource | `false` |
| `ingress.annotations` | Ingress annotations | `ingress.bluemix.net/redirect-to-https: "True"` |
| `ingress.hosts` | Hostname(s) to your spring app | `[]` |
| `ingress.tls.secretName` | Name of secret holding TLS certs | `nil` |
| `ingress.tls.hosts` | Hostname(s) to your spring app behind TLS | `[]` |
| `hpa.enabled` |  | `true` |
| `hpa.maxReplicas` |  | `2` |
| `hpa.minReplicas` |  | `1` |
| `hpa.metrics.cpu.targetAverageUtilization` |  | `70` |
| `hpa.metrics.memory.targetAverageUtilization` |  | `90` |
| `podAnnotations` | Annotations to apply to the pod | `{}` |
| `podAnnotations.downscaler/uptime` | Application uptime | `Mon-Fri 07:30-20:00 CET` |
| `image.repository`  | location of image to run | `nil` |
| `image.tag`         | **server** image tag | `nil` |
| `image.pullPolicy`  | **server** image pull policy | `IfNotPresent` |
| `livenessProbe.httpGet.path` | Values to enable livenessProbe suitable for your application | `/actuator/health` |
| `livenessProbe.httpGet.port` | Values to enable livenessProbe suitable for your application | `http` |
| `livenessProbe.initialDelaySeconds` | Values to enable livenessProbe suitable for your application | `60` |
| `livenessProbe.periodSeconds` | Values to enable livenessProbe suitable for your application | `10` |
| `readinessProbe.httpGet.path` | Values to enable livenessProbe suitable for your application | `/actuator/health` |
| `readinessProbe.httpGet.port` | Values to enable livenessProbe suitable for your application | `http` |
| `readinessProbe.initialDelaySeconds` | Values to enable livenessProbe suitable for your application | `60` |
| `readinessProbe.periodSeconds` | Values to enable livenessProbe suitable for your application | `10` |
| `pvc.enabled` |  | `false` |
| `pvc.storageClassName` | Value for storageClass to create PVC | `ibmc-s3fs-standard-standard-regional` |
| `containerPort` | the port your application listens on | `8080` |
| `extraEnv` | extra environment variables to pass to your application | `{}` |
| `securityContext.runAsUser` |  | `1000` |
| `securityContext.fsGroup` |  | `1000` |
| `nodeSelector` | Node labels for pod assignment | `{}` |
| `tolerations` | List of node taints to tolerate | `[]` |
| `affinity` | Pod affinity | `{}` |
| `podDisruptionBudget.enabled` |  | `true` |
| `podDisruptionBudget.minAvailable` |  | `1` |
| `istio.enabled` |  | `false` |
| `istio.stable.weight` | Istio virtual service weight | `100` |
| `istio.canary.weight` | Istio virtual service weight | `0` |
| `istio.gateway.host` | Isitio ingress gateway NLB hostname | `nil` |
| `istio.serviceentry.name` | Isitio external serviceentry | `nil` |
| `istio.serviceentry.host` | Isitio external serviceentry | `nil` |
| `istio.serviceentry.port` | Isitio external serviceentry | `nil` |
| `istio.serviceentry.protocol` | Isitio external serviceentry <http|https|TCP> | `nil` |