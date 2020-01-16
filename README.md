# Spring Chart

[Spring](http://spring.io/) is a modern Java framework.

## Chart Details

This chart is designed to be a general purpose chart for running Spring based applications.

## Add repo

To add repo with the name `stephane80000`:

```bash
$ helm repo add stephane80000 https://stephane80000.github.io/helm-charts/
$ helm repo update
```

## Installing the Chart

To install the chart with the release name `myapp` and a YAML file that specifies the values for the parameters `values-xxx.yaml` in the namespace `mynamespace` :

```bash
$ helm install myapp stephane80000/spring --version X.X.X -n mynamespace -f values-xxx.yaml
```

## Uninstalling the Chart

To uninstall/delete the `myapp` deployment:

```console
helm delete --purge myapp
```

The command removes nearly all the Kubernetes components associated with the
chart and deletes the release.

## Configuration

The following table lists the configurable parameters and their default values.

Alternatively, you can sepcify each parameter using the `--set key=value[,key=value]` argument to `helm install`.


> **Tip**: You can donwload the sample [spring/values.yaml](spring/values.yaml)

| Parameter | Description | Default |
|-----------|-------------|---------|
| `codeAP` | The application code | `nil` |
| `tier` |  | `nil` |
| `function` |  | `nil` |
| `version` |  | `current` |
| `replicaCount` | The number of replicas | `1` |
| `hpa.enabled` |  | `false` |
| `hpa.maxReplicas` |  | `3` |
| `hpa.minReplicas` |  | `1` |
| `hpa.metrics.cpu.targetAverageUtilization` |  | `70` |
| `hpa.metrics.memory.targetAverageUtilization` |  | `90` |
| `podAnnotations` | Annotations to apply to the pod | `{}` |
| `podAnnotations.downscaler/uptime` | Application uptime | `Mon-Fri 07:30-20:00 CET` |
| `image.repository`  | location of image to run | `de.icr.io` |
| `image.tag`         | **server** image tag | `0.0.1` |
| `image.pullPolicy`  | **server** image pull policy | `IfNotPresent` |
| `livenessProbe` | Values to enable livenessProbe suitable for your application | `{}` |
| `readinessProbe` | Values to enable readinessProbe suitable for your application | `{}` |
| `javaopts` |  | `-Dspring.profiles.active=cloud-dev -Dspring.config.additional-location=/applis/config/external-config.yml` |
| `secretRef.enabled` |  | `false` |
| `pvc.enabled` |  | `false` |
| `pvc.storageClassName` | Value for storageClass to create PVC | `ibmc-s3fs-standard-standard-regional` |
| `spring.config.content` | YAML to be placed in `/config/application.yml` | `nil` |
| `spring.config.clientCerts.enabled` | Load client certificate from secret `myapp-security` in /applis/security | `false` | 
| `containerPort` | the port your application listens on | `8080` |
| `extraEnv` | extra environment variables to pass to your application | `{}` |
| `securityContext.runAsUser` |  | `1000` |
| `securityContext.fsGroup` |  | `1000` |
| `resources` | Resource requests and limits | `{}` |
| `nodeSelector` | Node labels for pod assignment | `{}` |
| `tolerations` | List of node taints to tolerate | `[]` |
| `affinity` | Pod affinity | `{}` |
| `service.enabled` | Enable creating a service | `true` |
| `service.type` | Kubernetes Service type | `ClusterIP` |
| `service.httpPort`| Service HTTP port | `80` |
| `service.httpsPort`| Service HTTP port | `80` |
| `ingress.enabled` | Enable ingress controller resource | `false` |
| `ingress.annotations` | Ingress annotations | `ingress.bluemix.net/redirect-to-https: "True"` |
| `ingress.hosts` | Hostname(s) to your spring app | `[]` |
| `ingress.tls.secretName` | Name of secret holding TLS certs | `nil` |
| `ingress.tls.hosts` | Hostname(s) to your spring app behind TLS | `[]` |
| `podDisruptionBudget.enabled` |  | `false` |
| `podDisruptionBudget.podDisruptionBudget` |  | `1` |
| `istio.enabled` |  | `false` |
| `istio.current.weight` |  | `100` |
| `istio.canary.weight` |  | `0` |