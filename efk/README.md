# Elasticsearch Chart
This chart is based on the [elasticsearch/elasticsearch](https://www.docker.elastic.co/) image.
 
# Fluent-Bit Chart
[Fluent Bit](http://fluentbit.io/) is an open source and multi-platform Log Forwarder. 

This chart will do the following:
* Install a configmap for Fluent Bit
* Install a daemonset that provisions Fluent Bit [per-host architecture]

# kibana
[kibana](https://github.com/elastic/kibana) is your window into the Elastic Stack. Specifically, it's an open source (Apache Licensed), browser-based analytics and search dashboard for Elasticsearch.

# Configurations

## Elasticsearch

The following table lists the configurable parameters of the elasticsearch chart and their default values.

|              Parameter               |                             Description                             |                       Default                       |
| ------------------------------------ | ------------------------------------------------------------------- | --------------------------------------------------- |
| `appVersion`                         | Application Version (Elasticsearch)                                 | `6.5.3`                                             |
| `image.repository`                   | Container image name                                                | `docker.elastic.co/elasticsearch/elasticsearch-oss` |
| `image.tag`                          | Container image tag                                                 | `6.5.1`                                             |
| `image.pullPolicy`                   | Container pull policy                                               | `IfNotPresent`                                      |
| `initImage.repository`               | Init container image name                                           | `busybox`                                           |
| `initImage.tag`                      | Init container image tag                                            | `latest`                                            |
| `initImage.pullPolicy`               | Init container pull policy                                          | `Always`                                            |
| `cluster.name`                       | Cluster name                                                        | `elasticsearch`                                     |
| `cluster.xpackEnable`                | Writes the X-Pack configuration options to the configuration file   | `false`                                             |
| `cluster.config`                     | Additional cluster config appended                                  | `{}`                                                |
| `cluster.keystoreSecret`             | Name of secret holding secure config options in an es keystore      | `nil`                                               |
| `cluster.env`                        | Cluster environment variables                                       | `{MINIMUM_MASTER_NODES: "2"}`                       |
| `cluster.additionalJavaOpts`         | Cluster parameters to be added to `ES_JAVA_OPTS` environment variable | `""`                                              |
| `client.name`                        | Client component name                                               | `client`                                            |
| `client.replicas`                    | Client node replicas (deployment)                                   | `2`                                                 |
| `client.resources`                   | Client node resources requests & limits                             | `{} - cpu limit must be an integer`                 |
| `client.priorityClassName`           | Client priorityClass                                                | `nil`                                               |
| `client.podAnnotations`              | Client Deployment annotations                                       | `{}`                                                |
| `client.nodeSelector`                | Node labels for client pod assignment                               | `{}`                                                |
| `client.tolerations`                 | Client tolerations                                                  | `[]`                                                |
| `client.serviceAnnotations`          | Client Service annotations                                          | `{}`                                                |
| `client.serviceType`                 | Client service type                                                 | `ClusterIP`                                         |
| `client.loadBalancerIP`              | Client loadBalancerIP                                               | `{}`                                                |
| `client.loadBalancerSourceRanges`    | Client loadBalancerSourceRanges                                     | `{}`                                                |
| `client.antiAffinity`                | Client anti-affinity policy                                         | `soft`                                              |
| `client.nodeAffinity`                | Client node affinity policy                                         | `{}`                                                |
| `client.ingress.enabled`             | Enable Client Ingress                                               | `false`                                             |
| `client.ingress.annotations`         | Client Ingress annotations                                          | `{}`                                                |
| `client.ingress.hosts`               | Client Ingress Hostnames                                            | `[]`                                                |
| `client.ingress.tls`                 | Client Ingress TLS configuration                                    | `[]`                                                |
| `master.exposeHttp`                  | Expose http port 9200 on master Pods for monitoring, etc            | `false`                                             |
| `master.name`                        | Master component name                                               | `master`                                            |
| `master.replicas`                    | Master node replicas (deployment)                                   | `2`                                                 |
| `master.resources`                   | Master node resources requests & limits                             | `{} - cpu limit must be an integer`                 |
| `master.priorityClassName`           | Master priorityClass                                                | `nil`                                               |
| `master.podAnnotations`              | Master Deployment annotations                                       | `{}`                                                |
| `master.nodeSelector`                | Node labels for master pod assignment                               | `{}`                                                |
| `master.tolerations`                 | Master tolerations                                                  | `[]`                                                |
| `master.name`                        | Master component name                                               | `master`                                            |
| `master.persistence.enabled`         | Master persistent enabled/disabled                                  | `true`                                              |
| `master.persistence.name`            | Master statefulset PVC template name                                | `data`                                              |
| `master.persistence.size`            | Master persistent volume size                                       | `4Gi`                                               |
| `master.persistence.storageClass`    | Master persistent volume Class                                      | `nil`                                               |
| `master.persistence.accessMode`      | Master persistent Access Mode                                       | `ReadWriteOnce`                                     |
| `master.antiAffinity`                | Master anti-affinity policy                                         | `soft`                                              |
| `master.nodeAffinity`                | Master node affinity policy                                         | `{}`                                                |
| `master.updateStrategy`              | Master node update strategy policy                                  | `{type: "onDelete"}`                                |
| `data.exposeHttp`                    | Expose http port 9200 on data Pods for monitoring, etc              | `false`                                             |
| `data.replicas`                      | Data node replicas (statefulset)                                    | `2`                                                 |
| `data.resources`                     | Data node resources requests & limits                               | `{} - cpu limit must be an integer`                 |
| `data.priorityClassName`             | Data priorityClass                                                  | `nil`                                               |
| `data.hooks.drain.enabled            | Data nodes: Enable drain pre-stop and post-start hook               | `true`                                              |
| `data.persistence.enabled`           | Data persistent enabled/disabled                                    | `true`                                              |
| `data.persistence.name`              | Data statefulset PVC template name                                  | `data`                                              |
| `data.persistence.size`              | Data persistent volume size                                         | `30Gi`                                              |
| `data.persistence.storageClass`      | Data persistent volume Class                                        | `nil`                                               |
| `data.persistence.accessMode`        | Data persistent Access Mode                                         | `ReadWriteOnce`                                     |
| `data.podAnnotations`                | Data StatefulSet annotations                                        | `{}`                                                |
| `data.nodeSelector`                  | Node labels for data pod assignment                                 | `{}`                                                |
| `data.tolerations`                   | Data tolerations                                                    | `[]`                                                |
| `data.terminationGracePeriodSeconds` | Data termination grace period (seconds)                             | `3600`                                              |
| `data.antiAffinity`                  | Data anti-affinity policy                                           | `soft`                                              |
| `data.nodeAffinity`                  | Data node affinity policy                                           | `{}`                                                |
| `data.updateStrategy`                | Data node update strategy policy                                    | `{type: "onDelete"}`                                |
| `extraInitContainers`                | Additional init container passed through the tpl                    | ``                                                  |
| `podSecurityPolicy.annotations`      | Specify pod annotations in the pod security policy                  | `{}`                                                |
| `podSecurityPolicy.enabled`          | Specify if a pod security policy must be created                    | `false`                                             |
| `serviceAccounts.client.create`      | If true, create the client service account                          | `true`                                              |
| `serviceAccounts.client.name`        | Name of the client service account to use or create                 | `{{ elasticsearch.client.fullname }}`               |
| `serviceAccounts.master.create`      | If true, create the master service account                          | `true`                                              |
| `serviceAccounts.master.name`        | Name of the master service account to use or create                 | `{{ elasticsearch.master.fullname }}`               |
| `serviceAccounts.data.create`        | If true, create the data service account                            | `true`                                              |
| `serviceAccounts.data.name`          | Name of the data service account to use or create                   | `{{ elasticsearch.data.fullname }}`                 |



## Kibana

The following table lists the configurable parameters of the kibana chart and their default values.

| Parameter                                     | Description                                | Default                                |
|-----------------------------------------------|--------------------------------------------|----------------------------------------|
| `affinity`                                    | node/pod affinities                        | None                                   |
| `env`                                         | Environment variables to configure Kibana  | `{}`                                   |
| `files`                                       | Kibana configuration files                 | None                                   |
| `livenessProbe.enabled`                       | livenessProbe to be enabled?               | `false`                                |
| `livenessProbe.initialDelaySeconds`           | number of seconds                          | 30                                     |
| `livenessProbe.timeoutSeconds`                | number of seconds                          | 10                                     |
| `image.pullPolicy`                            | Image pull policy                          | `IfNotPresent`                         |
| `image.repository`                            | Image repository                           | `docker.elastic.co/kibana/kibana-oss`  |
| `image.tag`                                   | Image tag                                  | `6.5.3`                                |
| `image.pullSecrets`                           | Specify image pull secrets                 | `nil`                                  |
| `commandline.args`                            | add additional commandline args            | `nil`                                  |
| `ingress.enabled`                             | Enables Ingress                            | `false`                                |
| `ingress.annotations`                         | Ingress annotations                        | None:                                  |
| `ingress.hosts`                               | Ingress accepted hostnames                 | None:                                  |
| `ingress.tls`                                 | Ingress TLS configuration                  | None:                                  |
| `nodeSelector`                                | node labels for pod assignment             | `{}`                                   |
| `podAnnotations`                              | annotations to add to each pod             | `{}`                                   |
| `replicaCount`                                | desired number of pods                     | `1`                                    |
| `revisionHistoryLimit`                        | revisionHistoryLimit                       | `3`                                    |
| `serviceAccountName`                          | DEPRECATED: use serviceAccount.name        | `nil`                                  |
| `serviceAccount.create`                       | create a serviceAccount to run the pod     | `false`                                |
| `serviceAccount.name`                         | name of the serviceAccount to create       | `kibana.fullname`                      |
| `authProxyEnabled`                            | enables authproxy. Create container in extracontainers   | `false`                  |
| `extraContainers`                             | Sidecar containers to add to the kibana pod| `{}`                                   |
| `resources`                                   | pod resource requests & limits             | `{}`                                   |
| `priorityClassName`                           | priorityClassName                          | `nil`                                  |
| `service.externalPort`                        | external port for the service              | `443`                                  |
| `service.internalPort`                        | internal port for the service              | `4180`                                 |
| `service.authProxyPort`                       | port to use when using sidecar authProxy   | None:                                  |
| `service.externalIPs`                         | external IP addresses                      | None:                                  |
| `service.loadBalancerIP`                      | Load Balancer IP address                   | None:                                  |
| `service.loadBalancerSourceRanges`            | Limit load balancer source IPs to list of CIDRs (where available)) | `[]`           |
| `service.nodePort`                            | NodePort value if service.type is NodePort | None:                                  |
| `service.type`                                | type of service                            | `ClusterIP`                            |
| `service.annotations`                         | Kubernetes service annotations             | None:                                  |
| `service.labels`                              | Kubernetes service labels                  | None:                                  |
| `tolerations`                                 | List of node taints to tolerate            | `[]`                                   |
| `dashboardImport.timeout`                     | Time in seconds waiting for Kibana to be in green overall state | `60`                                   |
| `dashboardImport.xpackauth.enabled`           | Enable Xpack auth                          | `false`                                |
| `dashboardImport.xpackauth.username`          | Optional Xpack username                    | `myuser`                               |
| `dashboardImport.xpackauth.password`          | Optional Xpack password                    | `mypass`                               |
| `dashboardImport.dashboards`                  | Dashboards                                 | `{}`                                   |
| `plugins.enabled`                             | Enable installation of plugins.            | `false`                                |
| `plugins.reset`                               | Optional : Remove all installed plugins before installing all new ones | `false`                                   |
| `plugins.values`                              | List of plugins to install. Format <pluginName,version,URL> with URLs pointing to zip files of Kibana plugins to install                                 | None:                                   |
| `persistentVolumeClaim.enabled`               | Enable PVC for plugins                     | `false`                                 |
| `persistentVolumeClaim.existingClaim`         | Use your own PVC for plugins               | `false`                                 |
| `persistentVolumeClaim.annotations`           | Add your annotations for the PVC           | `{}`                                    |
| `persistentVolumeClaim.accessModes`           | Acces mode to the PVC                      | `ReadWriteOnce`                         |
| `persistentVolumeClaim.size`                  | Size of the PVC                            | `5Gi`                                   |
| `persistentVolumeClaim.storageClass`          | Storage class of the PVC                   | None:                                   |
| `readinessProbe.enabled`                      | readinessProbe to be enabled?              | `false`                                 |
| `readinessProbe.initialDelaySeconds`          | number of seconds                          | 30                                      |
| `readinessProbe.timeoutSeconds`               | number of seconds                          | 10                                      |
| `readinessProbe.periodSeconds`                | number of seconds                          | 10                                      |
| `readinessProbe.successThreshold`             | number of successes                        | 5                                       |
| `securityContext.enabled`                     | Enable security context (should be true for PVC)                    | `false`                                  |
| `securityContext.allowPrivilegeEscalation`    | Allow privilege escalation                 | `false`                                 |
| `securityContext.runAsUser`                   | User id to run in pods                     | `1000`                                  |
| `securityContext.fsGroup`                     | fsGroup id to run in pods                  | `2000`                                  |
| `extraConfigMapMounts`                        | Additional configmaps to be mounted        | `[]`                                    |



## Fluent-Bit

The following table lists the configurable parameters of the Fluent-Bit chart and the default values.

| Parameter                  | Description                        | Default                 |
| -----------------------    | ---------------------------------- | ----------------------- |
| **Backend Selection**      |
| `backend.type`             | Set the backend to which Fluent-Bit should flush the information it gathers | `forward` |
| **Forward Backend**        |
| `backend.forward.host`     | Target host where Fluent-Bit or Fluentd are listening for Forward messages | `fluentd` |
| `backend.forward.port`     | TCP Port of the target service | `24284` |
| `backend.forward.shared_key`       | A key string known by the remote Fluentd used for authorization. | `` |
| `backend.forward.tls`              | Enable or disable TLS support | `off` |
| `backend.forward.tls_verify`       | Force certificate validation  | `on` |
| `backend.forward.tls_debug`        | Set TLS debug verbosity level. It accept the following values: 0-4 | `1` |
| **ElasticSearch Backend**  |
| `backend.es.host`          | IP address or hostname of the target Elasticsearch instance | `elasticsearch` |
| `backend.es.port`          | TCP port of the target Elasticsearch instance. | `9200` |
| `backend.es.index`         | Elastic Index name | `kubernetes_cluster` |
| `backend.es.type`          | Elastic Type name | `flb_type` |
| `backend.es.time_key`          | Elastic Time Key | `@timestamp` |
| `backend.es.logstash_prefix`  | Index Prefix. If Logstash_Prefix is equals to 'mydata' your index will become 'mydata-YYYY.MM.DD'. | `kubernetes_cluster` |
| `backend.es.replace_dots`     | Enable/Disable Replace_Dots option. | `On` |
| `backend.es.http_user`        | Optional username credential for Elastic X-Pack access. | `` |
| `backend.es.http_passwd:`     | Password for user defined in HTTP_User. | `` |
| `backend.es.tls`              | Enable or disable TLS support | `off` |
| `backend.es.tls_verify`       | Force certificate validation  | `on` |
| `backend.es.tls_ca`           | TLS CA certificate for the Elastic instance (in PEM format). Specify if tls: on. | `` |
| `backend.es.tls_debug`        | Set TLS debug verbosity level. It accept the following values: 0-4 | `1` |
| **HTTP Backend**              |
| `backend.http.host`           | IP address or hostname of the target HTTP Server | `127.0.0.1` |
| `backend.http.port`           | TCP port of the target HTTP Server | `80` |
| `backend.http.uri`            | Specify an optional HTTP URI for the target web server, e.g: /something | `"/"`
| `backend.http.http_user`        | Optional username credential for Basic Authentication. | `` |
| `backend.http.http_passwd:`     | Password for user defined in HTTP_User. | `` |
| `backend.http.format`         | Specify the data format to be used in the HTTP request body, by default it uses msgpack, optionally it can be set to json.  | `msgpack` |
| `backend.http.tls`              | Enable or disable TLS support | `off` |
| `backend.http.tls_verify`       | Force certificate validation  | `on` |
| `backend.http.tls_debug`        | Set TLS debug verbosity level. It accept the following values: 0-4 | `1` |
| **Splunk Backend**              |
| `backend.splunk.host`           | IP address or hostname of the target Splunk Server | `127.0.0.1` |
| `backend.splunk.port`           | TCP port of the target Splunk Server | `8088` |
| `backend.splunk.token`            | Specify the Authentication Token for the HTTP Event Collector interface. | `` |
| `backend.splunk.send_raw`         | If enabled, record keys and values are set in the main map. | `off` |
| `backend.splunk.tls`           | Enable or disable TLS support | `on` |
| `backend.splunk.tls_verify`           | Force TLS certificate validation | `off` |
| `backend.splunk.tls_debug`        | Set TLS debug verbosity level. It accept the following values: 0-4 | `1` |
| `backend.splunk.message_key`           | Tag applied to all incoming logs | `kubernetes` |
| **Parsers**                   |
| `parsers.enabled`                  | Enable custom parsers | `false` |
| `parsers.regex`                    | List of regex parsers | `NULL` |
| `parsers.json`                     | List of json parsers | `NULL` |
| **General**                   |
| `annotations`                      | Optional deamonset set annotations        | `NULL`                |
| `podAnnotations`                   | Optional pod annotations                  | `NULL`                |
| `fullConfigMap`                    | User has provided entire config (parsers + system)  | `false`      |
| `existingConfigMap`                | ConfigMap override                         | ``                    |
| `extraEntries.input`               |    Extra entries for existing [INPUT] section                     | ``                    |
| `extraEntries.filter`               |    Extra entries for existing [FILTER] section                     | ``                    |
| `extraEntries.output`               |   Extra entries for existing [OUPUT] section                     | ``                    |
| `extraPorts`                       | List of extra ports                        |                       |
| `extraVolumeMounts`                | Mount an extra volume, required to mount ssl certificates when elasticsearch has tls enabled |          |
| `extraVolume`                      | Extra volume                               |                                                |
| `filter.enableExclude`                   | Enable the use of monitoring for a pod annotation of `fluentbit.io/exclude: true`. If present, discard logs from that pod.         | `true`                                 |
| `filter.enableParser`                   | Enable the use of monitoring for a pod annotation of `fluentbit.io/parser: parser_name`. parser_name must be the name of a parser contained within parsers.conf         | `true`                                 |
| `filter.kubeURL`                   | Optional custom configmaps                 | `https://kubernetes.default.svc:443`            |
| `filter.kubeCAFile`                | Optional custom configmaps       | `/var/run/secrets/kubernetes.io/serviceaccount/ca.crt`    |
| `filter.kubeTokenFile`             | Optional custom configmaps       | `/var/run/secrets/kubernetes.io/serviceaccount/token`     |
| `filter.kubeTag`                   | Optional top-level tag for matching in filter         | `kube`                                 |
| `filter.mergeJSONLog`                   | If the log field content is a JSON string map, append the map fields as part of the log structure         | `true`                                 |
| `image.fluent_bit.repository`      | Image                                      | `fluent/fluent-bit`                               |
| `image.fluent_bit.tag`             | Image tag                                  | `1.0.1`                                          |
| `image.pullPolicy`                 | Image pull policy                          | `Always`                                          |
| `image.pullSecrets`                | Specify image pull secrets                 | `nil`                                             |
| `input.tail.memBufLimit`           | Specify Mem_Buf_Limit in tail input        | `5MB`                                             |
| `input.tail.path`           | Specify log file(s) through the use of common wildcards.        | `/var/log/containers/*.log`                                             |
| `rbac.create`                      | Specifies whether RBAC resources should be created.   | `true`                                 |
| `serviceAccount.create`            | Specifies whether a ServiceAccount should be created. | `true`                                 |
| `serviceAccount.name`              | The name of the ServiceAccount to use.     | `NULL`                                            |
| `rawConfig`                        | Raw contents of fluent-bit.conf            | `@INCLUDE fluent-bit-service.conf`<br>`@INCLUDE fluent-bit-input.conf`<br>`@INCLUDE fluent-bit-filter.conf`<br>` @INCLUDE fluent-bit-output.conf`                                                                         |
| `resources`                        | Pod resource requests & limits                                 | `{}`                          |
| `hostNetwork`                      | Use host's network                         | `false`                                           |
| `dnsPolicy`                        | Specifies the dnsPolicy to use             | `ClusterFirst`                                    |
| `tolerations`                      | Optional daemonset tolerations             | `NULL`                                            |
| `nodeSelector`                     | Node labels for fluent-bit pod assignment  | `NULL`                                            |
| `metrics.enabled`                  | Specifies whether a service for metrics should be exposed | `false`                            |
| `metrics.service.annotations`      | Optional metrics service annotations       | `NULL`                                            |
| `metrics.service.port`             | Port on where metrics should be exposed    | `2020`                                            |
| `metrics.service.type`             | Service type for metrics                   | `ClusterIP`                                       |
| `trackOffsets`                     | Specify whether to track the file offsets for tailing docker logs. This allows fluent-bit to pick up where it left after pod restarts but requires access to a `hostPath` | `false` |
| | | |
