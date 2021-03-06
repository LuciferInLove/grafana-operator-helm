# grafana-operator

Installs [grafana-operator](https://github.com/integr8ly/grafana-operator).

The default installation creates the operator deployment, installs crds and creates Grafana custom resource. See examples in values.yaml to create GrafanaDashboard and GrafanaDatasource custom resources.

## Installing the Chart

```
kubectl create ns grafana
helm install grafana-operator ./ --namespace grafana
```

## Chart Values

| Parameter | Type | Default | Description |
|-----|------|---------|-------------|
| operator.replicas | int | `1` | Operator deployment replicas. |
| operator.image.repository | string | `quay.io/integreatly/grafana-operator` | Repository for grafana operator image. |
| operator.image.tag | string | `v3.4.0` | Tag for grafana operator image. |
| operator.image.pullPolicy | string | `IfNotPresent` | Grafana operator image pull policy. |
| operator.createCustomResources | bool | `false` | Create CRDs. If you are using Helm version < 2.10 you will have to either create the CRDs first. Helm v3+ will create the CRDs if those are not present already regardless of this value. Use `--skip-crds` with `helm install` for Helm v3+ if you want to skip CRD creation. |
| operator.args | list | `[]` | Arguments that can be passed to the grafana operator command. |
| operator.deploymentStrategy | object | `{"type": "Recreate"}` | Operator deployment strategy. |
| operator.podLabels | object | `{}` | Operator pod labels. |
| operator.podAnnotations | object | `{}` | Operator pod annotations. |
| operator.podSecurityContext | object | `{}` | Operator pod security context. |
| operator.nodeSelector | object | `{}` | Labels of nodes on which operator pod is scheduled on. |
| operator.tolerations | list | `[]` | Tolerations for use with node taints. |
| operator.affinity | object | `{}` | Affinity rules of the operator pod. |
| operator.containerSecurityContext | object | `{}` | Operator container security context. |
| operator.containerPort | int | `8080` | Operator metrics container port. |
| operator.watchNamespace | string | `""` | Namespace that grafana operator watches. If not defined, operator deployment namespace will be used. |
| operator.templatePath | string | `/usr/local/bin/templates` | Operator's templates path inside container. |
| operator.serviceAccount.create | bool | `true` | Create grafana operator deployment service account. |
| operator.serviceAccount.name | string | `""` | Override service account name. Defaults to release name. |
| operator.serviceAccount.annotations | object | `{}` | Annotations to add to service account. |
| operator.monitoring.enabled | bool | `false` | Create grafana operator ServiceMonitor. |
| operator.monitoring.namespace | string | `monitoring` | ServiceMonitor namespace. |
| operator.monitoring.interval | string | `15s` | ServiceMonitor scrape interval. |
| operator.monitoring.path | string | `/metrics` | Operator's metrics endpoint path. |
| operator.monitoring.port | string | `http-metrics` | Operator's metrics service port. |
| operator.monitoring.relabelings | list | `[]` | ServiceMonitor endpoint relabelings. |
| grafana[0].name | string | `grafana` | Name of Grafana instance. |
| grafana[0].baseImage | string | `""` | Custom grafana image for the grafana deployment. Warning! This overwrites the `--grafana-image` operator flag. |
| grafana[0].initImage | string | `""` | Custom grafana plugins init image for the grafana deployment. Warning! This overwrites the `--grafana-plugins-init-container-image` operator flag. |
| grafana[0].containers | list | `[]` | Additional containers to add to the grafana pod. |
| grafana[0].secrets | list | `[]` | Secrets to be mounted as volume into the grafana deployment. |
| grafana[0].configMaps | list | `[]` | ConfigMaps to be mounted as volume into the grafana deployment. |
| grafana[0].initResources | object | `{}` | Describes init compute resource requirements. |
| grafana[0].resources | object | `{}` | Describes compute resource requirements. |
| grafana[0].logLevel | string | `warn` | Log level of the grafana instance. Defaults to info if not defined. |
| grafana[0].adminUser | string | `admin` | Default admin user name of the grafana instance. |
| grafana[0].adminPassword | string | `admin` | Default admin user password of the grafana instance. |
| grafana[0].basicAuth | bool | `true` | Defines if basic auth enabled. |
| grafana[0].disableLoginForm | bool | `false` | Disables grafana instance's login form. |
| grafana[0].disableSignoutMenu | bool | `false` | Disables grafana instance's signout menu. |
| grafana[0].anonymous | bool | `true` | Disables or enables anonymous login. |
| grafana[0].ingress.enabled | bool | `false` | Defines if grafana instance's ingress is enabled. |
| grafana[0].ingress.path | string | `""` | Grafana instance's ingress path. |
| grafana[0].ingress.pathTemplated | bool | `false` | Defines if ingress path uses go templates. |
| grafana[0].ingress.hostname | string | `""` | Grafana instance's ingress hostname. |
| grafana[0].ingress.hostnameTemplated | bool | `false` | Defines if ingress hostname uses go templates. |
| grafana[0].ingress.annotations | object | `{}` | Grafana instance's ingress annotations. |
| grafana[0].ingress.labels | object | `{}` | Grafana instance's ingress labels. |
| grafana[0].ingress.targetPort | string | `""` | Target port of grafana instance's ingress. |
| grafana[0].ingress.tlsEnabled | bool | `false` | Enables or disables tls for the ingress. |
| grafana[0].ingress.tlsSecretName | string | `""` | Name of the ingress certificate secret. |
| grafana[0].ingress.termination | string | `""` | Used in Openshift, dictates where the secure communication will stop. |
| grafana[0].service.enabled | bool | `true` | Defines if grafana instance's service is enabled. |
| grafana[0].service.name | string | `grafana-service` | Configurable name for the grafana's service. |
| grafana[0].service.ports | list | `[{"name": "grafana", "port": 3000, "protocol": "TCP", "targetPort": "grafana-http"}]` | Grafana instance's service ports. |
| grafana[0].service.annotations | object | `{}` | Grafana instance's service annotations. |
| grafana[0].service.labels | object | `{}` | Grafana instance's service labels. |
| grafana[0].service.type | string | `ClusterIP` | Grafana instance's service type. |
| grafana[0].service.clusterIP | string | `""` | Specifies your own cluster IP address for the grafana's service. |
| grafana[0].client | object | `{"preferService": true}` | Grafana client settings. |
| grafana[0].compat | object | `{}` | Grafana's backwards compatibility switches. |
| grafana[0].serviceAccount.skip | bool | `false` | Skips the grafana's ServiceAccount creation. |
| grafana[0].serviceAccount.annotations | object | `{}` | Additional annotations for ServiceAccount. |
| grafana[0].serviceAccount.labels | object | `{}` | Additional labels for ServiceAccount. |
| grafana[0].serviceAccount.imagePullSecrets | array | `[]` | Additional image pull secrets for ServiceAccount. |
| grafana[0].deployment.replicas | int | `1` | Grafana instance's replicas. |
| grafana[0].deployment.terminationGracePeriodSeconds | string | `""` | Grafana deployment termination grace period. |
| grafana[0].deployment.nodeSelector | object | `{}` | Labels of nodes on which grafana pods are scheduled on. |
| grafana[0].deployment.tolerations | list | `[]` | Additonal labels for running grafana pods in tained nodes. |
| grafana[0].deployment.affinity | object | `{}` | Additonal labels for running grafana pods with affinity properties. |
| grafana[0].deployment.securityContext | object | `{"runAsUser": 472, "runAsGroup": 472}` | Security Context for grafana pods. |
| grafana[0].deployment.containerSecurityContext | object | `{"runAsUser": 472, "runAsGroup": 472}` | Security Context for grafana pods containers. |
| grafana[0].config | object | `{"server": {"protocol": "http", "serve_from_sub_path": True}, "security": {"login_remember_days": 365}, "log": {"mode": "console"}, "users":{"allow_sign_up": False}}` | Config of the grafana instance. |
| grafana[0].configTemplated | bool | `false` | Defines if grafana instance's config uses go templates. |
| grafana[0].dashboardLabelSelector | list | `[{"matchExpressions": [{"key": "app", "operator": "In", "values": ["grafana"]}]}]` | Label selector or match expressions for grafana dashboards. |
| grafana[0].dashboardNamespaceSelector | object | `{}` | Namespace selector for grafana dashboards. |
| grafana[0].dataStorage.enabled | bool | `false` | Defines if grafana instance's data storage is enabled. If defined, grafana operator will create PersistentVolume and PersistentVolume claim for the grafana instance. |
| grafana[0].dataStorage.annotations | object | `{}` | Additional annotations for the grafana instance's data storage. |
| grafana[0].dataStorage.labels | object | `{}` | Additional labels for the grafana instance's data storage. |
| grafana[0].dataStorage.accessModes | list | `[]` | List of the persistent volume access modes. |
| grafana[0].dataStorage.size | string | `""` | Grafana instance's persistent volume size. |
| grafana[0].dataStorage.class | string | `""` | Grafana instance's persistent volume storage class. |
| grafana[0].jsonnet | object | `{}` | Label selector for jsonnet libraries. |
| grafana[0].livenessProbeSpec | object | `{}` | Liveness probe configuration for the grafana container. |
| grafana[0].readinessProbeSpec | object | `{}` | Readiness probe configuration for the grafana container. |
| grafanaDataSource | list | `[]` | List of GrafanaDataSource objects. See an example in values.yaml. |
| grafanaDashboard | list | `[]` | List of GrafanaDashboard objects. See an example in values.yaml. |
