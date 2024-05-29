# Maxai Agents
Using this marketplace product, you can deploy a Q&A agent named Maverick, which supports unstructured file formats such as PDFs, .docs, and more. 
The following features are available in Maverick: 
- Supports multiple file formats like PDF, docs, markdown, CSV, etc. 
- Works with unstructured data 
- Can create collections and default prompts 

## Introduction
Using the Helm package manager, this chart deploys the maxai agent operator on a Kubernetes cluster.

## TL;DR
```
helm install maverick \
    --namespace maxai-agent ./* \
    --set backend.serviceAccount.annotations=eks.amazonaws.com/role-arn: <<Replace with iam role created for s3>> \
    --set backend.resources.limits.memory=4Gi \
    --set backend.ingress.hosts.host=agent-01.max.local \
    --set ui.ingress.hosts.host=agent-01.max.local \
    --set backend.ingress.hosts.paths.path=/fastapi \
    --set ui.ingress.hosts.paths.path=/
```

## Requirements
- Kubernetes 1.23+
- Helm 3.8.0+
- LLM provider creds
- VectorStore
- ESO installation if want to integrate with External Secret Manager


## Parameters
----------------------------------------------------------------------------------------------------------------------------------------------
## Global parameters

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| global.aws.images.backend.image | string | `"maxai-agent-backend"` |  |
| global.aws.images.backend.pullPolicy | string | `"Always"` |  |
| global.aws.images.backend.registry | string | `"709825985650.dkr.ecr.us-east-1.amazonaws.com/zs-personalize-ai"` |  |
| global.aws.images.backend.tag | string | `"2.1.22"` |  |
| global.aws.images.controllerManager.image | string | `"maxai-agent-operator"` |  |
| global.aws.images.controllerManager.pullPolicy | string | `"Always"` |  |
| global.aws.images.controllerManager.registry | string | `"709825985650.dkr.ecr.us-east-1.amazonaws.com/zs-personalize-ai"` |  |
| global.aws.images.controllerManager.tag | string | `"1.8.2"` |  |
| global.aws.images.kubeRbacProxy.image | string | `"maxai-agent-kuberbac-proxy"` |  |
| global.aws.images.kubeRbacProxy.pullPolicy | string | `"IfNotPresent"` |  |
| global.aws.images.kubeRbacProxy.registry | string | `"709825985650.dkr.ecr.us-east-1.amazonaws.com/zs-personalize-ai"` |  |
| global.aws.images.kubeRbacProxy.tag | string | `"0.16.1"` |  |
| global.aws.images.maxaiparser.image | string | `"maxai-agent-parser"` |  |
| global.aws.images.maxaiparser.pullPolicy | string | `"IfNotPresent"` |  |
| global.aws.images.maxaiparser.registry | string | `"709825985650.dkr.ecr.us-east-1.amazonaws.com/zs-personalize-ai"` |  |
| global.aws.images.maxaiparser.tag | string | `"1.0.0"` |  |
| global.aws.images.postHook.image | string | `"kubectl"` |  |
| global.aws.images.postHook.pullPolicy | string | `"IfNotPresent"` |  |
| global.aws.images.postHook.registry | string | `"709825985650.dkr.ecr.us-east-1.amazonaws.com/zs-personalize-ai"` |  |
| global.aws.images.postHook.tag | string | `"1.0.0"` |  |
| global.aws.images.postgresql.image | string | `"maxai-postgres"` |  |
| global.aws.images.postgresql.pullPolicy | string | `"IfNotPresent"` |  |
| global.aws.images.postgresql.registry | string | `"709825985650.dkr.ecr.us-east-1.amazonaws.com/zs-personalize-ai"` |  |
| global.aws.images.postgresql.tag | int | `16` |  |
| global.aws.images.redis.image | string | `"maxai-redis"` |  |
| global.aws.images.redis.pullPolicy | string | `"IfNotPresent"` |  |
| global.aws.images.redis.registry | string | `"709825985650.dkr.ecr.us-east-1.amazonaws.com/zs-personalize-ai"` |  |
| global.aws.images.redis.tag | string | `"7.2.4"` |  |
| global.aws.images.ui.image | string | `"maxai-agents-ui"` |  |
| global.aws.images.ui.pullPolicy | string | `"Always"` |  |
| global.aws.images.ui.registry | string | `"709825985650.dkr.ecr.us-east-1.amazonaws.com/zs-personalize-ai"` |  |
| global.aws.images.ui.tag | string | `"v1"` |  |
| spec.registry | object | `{}` |  |
| spec.securityContext | object | `{}` |  |
| spec.securityContexts | object | `{}` |  |
| spec.nodeSelector | object | `{}` |  |

## Operator parameters

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| operator.controllerManager.affinity | list | `[]` |  |
| operator.controllerManager.imagePullSecrets[0].name | string | `"maxai-repo-secret"` |  |
| operator.controllerManager.kubeRbacProxy.args[0] | string | `"--secure-listen-address=0.0.0.0:8443"` |  |
| operator.controllerManager.kubeRbacProxy.args[1] | string | `"--upstream=http://127.0.0.1:8080/"` |  |
| operator.controllerManager.kubeRbacProxy.args[2] | string | `"--logtostderr=true"` |  |
| operator.controllerManager.kubeRbacProxy.args[3] | string | `"--v=0"` |  |
| operator.controllerManager.kubeRbacProxy.containerSecurityContext.allowPrivilegeEscalation | bool | `false` |  |
| operator.controllerManager.kubeRbacProxy.containerSecurityContext.capabilities.drop[0] | string | `"ALL"` |  |
| operator.controllerManager.kubeRbacProxy.resources.limits.cpu | string | `"2"` |  |
| operator.controllerManager.kubeRbacProxy.resources.limits.memory | string | `"4Gi"` |  |
| operator.controllerManager.kubeRbacProxy.resources.requests.cpu | string | `"1"` |  |
| operator.controllerManager.kubeRbacProxy.resources.requests.memory | string | `"2Gi"` |  |
| operator.controllerManager.manager.args[0] | string | `"--health-probe-bind-address=:8081"` |  |
| operator.controllerManager.manager.args[1] | string | `"--metrics-bind-address=127.0.0.1:8080"` |  |
| operator.controllerManager.manager.args[2] | string | `"--leader-elect"` |  |
| operator.controllerManager.manager.args[3] | string | `"--leader-election-id=maxai-agents"` |  |
| operator.controllerManager.manager.containerSecurityContext.allowPrivilegeEscalation | bool | `false` |  |
| operator.controllerManager.manager.containerSecurityContext.capabilities.drop[0] | string | `"ALL"` |  |
| operator.controllerManager.manager.imagePullPolicy | string | `"IfNotPresent"` |  |
| operator.controllerManager.manager.resources.limits.cpu | string | `"2"` |  |
| operator.controllerManager.manager.resources.limits.memory | string | `"6Gi"` |  |
| operator.controllerManager.manager.resources.requests.cpu | string | `"1"` |  |
| operator.controllerManager.manager.resources.requests.memory | string | `"2Gi"` |  |
| operator.controllerManager.nodeSelector | list | `[]` |  |
| operator.controllerManager.replicas | int | `1` |  |
| operator.controllerManager.service.port | int | `80` |  |
| operator.controllerManager.service.type | string | `"ClusterIP"` |  |
| operator.controllerManager.tolerations | list | `[]` |  |
| operator.controllerServiceAccount.create | bool | `true` |  |
| operator.controllerServiceAccount.serviceAccount.annotations | object | `{}` |  |
| operator.enabled | bool | `true` |  |
| operator.installHooks | bool | `true` |  |
| operator.kubernetesClusterDomain | string | `"cluster.local"` |  |
| operator.rbac.create | bool | `true` |  |

## Backend Parameters

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| spec.backend.affinity | object | `{}` |  |
| spec.backend.allowPodLogReading | bool | `true` |  |
| spec.backend.annotations | object | `{}` |  |
| spec.backend.args | list | `[]` |  |
| spec.backend.command | string | `nil` |  |
| spec.backend.configMapAnnotations | object | `{}` |  |
| spec.backend.deployment.enabled | bool | `true` |  |
| spec.backend.enabled | bool | `true` |  |
| spec.backend.env | list | `[]` |  |
| spec.backend.envFrom.ENV | string | `"test"` |  |
| spec.backend.envFromSecret | string | `"{{ template \"maxai.fullname\" . }}-env"` |  |
| spec.backend.extraContainers | list | `[]` |  |
| spec.backend.hostAliases | list | `[]` |  |
| spec.backend.hpa.apiVersion | string | `"autoscaling/v2"` |  |
| spec.backend.hpa.behavior | object | `{}` |  |
| spec.backend.hpa.enabled | bool | `true` |  |
| spec.backend.hpa.maxReplicaCount | int | `5` |  |
| spec.backend.hpa.metrics[0].resource.name | string | `"cpu"` |  |
| spec.backend.hpa.metrics[0].resource.target.averageUtilization | int | `80` |  |
| spec.backend.hpa.metrics[0].resource.target.type | string | `"Utilization"` |  |
| spec.backend.hpa.metrics[0].type | string | `"Resource"` |  |
| spec.backend.hpa.minReplicaCount | int | `1` |  |
| spec.backend.ingress.annotations."cert-manager.io/cluster-issuer" | string | `"letsencrypt-prod-nginx"` |  |
| spec.backend.ingress.annotations."ingress.kubernetes.io/ssl-redirect" | string | `"true"` |  |
| spec.backend.ingress.annotations."kubernetes.io/tls-acme" | string | `"true"` |  |
| spec.backend.ingress.annotations."nginx.ingress.kubernetes.io/rewrite-target" | string | `"/$2"` |  |
| spec.backend.ingress.className | string | `"nginx"` |  |
| spec.backend.ingress.enabled | bool | `false` |  |
| spec.backend.ingress.hosts[0].host | string | `"agent-01.max.local"` |  |
| spec.backend.ingress.hosts[0].paths[0].path | string | `"/fastapi(/|$)(.*)"` |  |
| spec.backend.ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| spec.backend.ingress.tls[0].hosts[0] | string | `"agent-01.max.local"` |  |
| spec.backend.ingress.tls[0].secretName | string | `"agent-01-max-ui-tls"` |  |
| spec.backend.initContainers | list | `[]` |  |
| spec.backend.keda.advanced | object | `{}` |  |
| spec.backend.keda.apiVersion | string | `"keda.sh/v1alpha1"` |  |
| spec.backend.keda.cooldownPeriod | int | `30` |  |
| spec.backend.keda.enabled | bool | `false` |  |
| spec.backend.keda.maxReplicaCount | int | `10` |  |
| spec.backend.keda.minReplicaCount | int | `0` |  |
| spec.backend.keda.namespaceLabels | object | `{}` |  |
| spec.backend.keda.pollingInterval | int | `5` |  |
| spec.backend.keda.triggers | object | `{}` |  |
| spec.backend.labels | object | `{}` |  |
| spec.backend.livenessProbe.failureThreshold | int | `5` |  |
| spec.backend.livenessProbe.initialDelaySeconds | int | `15` |  |
| spec.backend.livenessProbe.periodSeconds | int | `10` |  |
| spec.backend.livenessProbe.scheme | string | `"HTTP"` |  |
| spec.backend.livenessProbe.timeoutSeconds | int | `5` |  |
| spec.backend.nodeSelector | object | `{}` |  |
| spec.backend.persistence.accessModes | string | `"ReadWriteOnce"` |  |
| spec.backend.persistence.annotations | object | `{}` |  |
| spec.backend.persistence.containerLifecycleHooks | object | `{}` |  |
| spec.backend.persistence.enabled | bool | `false` |  |
| spec.backend.persistence.fixPermissions | bool | `false` |  |
| spec.backend.persistence.name | string | `"model-data"` |  |
| spec.backend.persistence.securityContexts.container | object | `{}` |  |
| spec.backend.persistence.size | string | `"20Gi"` |  |
| spec.backend.persistence.storageClassName | string | `"gp2"` |  |
| spec.backend.ports.containerPort | int | `80` |  |
| spec.backend.ports.protocol | string | `"http"` |  |
| spec.backend.readinessProbe.failureThreshold | int | `5` |  |
| spec.backend.readinessProbe.initialDelaySeconds | int | `15` |  |
| spec.backend.readinessProbe.periodSeconds | int | `10` |  |
| spec.backend.readinessProbe.scheme | string | `"HTTP"` |  |
| spec.backend.readinessProbe.timeoutSeconds | int | `5` |  |
| spec.backend.replicas | int | `1` |  |
| spec.backend.resources.limits.cpu | string | `"100m"` |  |
| spec.backend.resources.limits.memory | string | `"128Mi"` |  |
| spec.backend.resources.requests.cpu | string | `"100m"` |  |
| spec.backend.resources.requests.memory | string | `"128Mi"` |  |
| spec.backend.secrets.connections.db_host | string | `"{{ .Release.Name }}-postgresql"` |  |
| spec.backend.secrets.connections.db_name | string | `"maxaiagent"` |  |
| spec.backend.secrets.connections.db_pass | string | `""` |  |
| spec.backend.secrets.connections.db_port | string | `"5432"` |  |
| spec.backend.secrets.connections.db_user | string | `"maxaiagent"` |  |
| spec.backend.secrets.connections.maxaiparser | string | `""` |  |
| spec.backend.secrets.connections.redis_cache_db | string | `""` |  |
| spec.backend.secrets.connections.redis_host | string | `"{{ .Release.Name }}-redis-headless"` |  |
| spec.backend.secrets.connections.redis_password | string | `"maxaiagent"` |  |
| spec.backend.secrets.connections.redis_port | string | `"6379"` |  |
| spec.backend.secrets.connections.redis_ssl.enabled | bool | `false` |  |
| spec.backend.secrets.connections.redis_ssl.ssl_cert_reqs | string | `"CERT_NONE"` |  |
| spec.backend.secrets.connections.redis_user | string | `""` |  |
| spec.backend.secrets.enabled | bool | `true` |  |
| spec.backend.secrets.extraSecretEnv | object | `{}` |  |
| spec.backend.secrets.secret.create | bool | `true` |  |
| spec.backend.secrets.vectordb.host | string | `"{{ .Release.Name }}-postgresql"` |  |
| spec.backend.secrets.vectordb.name | string | `"maxaiagent"` |  |
| spec.backend.secrets.vectordb.password | string | `"maxaiagent"` |  |
| spec.backend.secrets.vectordb.port | string | `"5432"` |  |
| spec.backend.secrets.vectordb.type | string | `"pgvector"` |  |
| spec.backend.secrets.vectordb.user | string | `"maxaiagent"` |  |
| spec.backend.service.annotations | object | `{}` |  |
| spec.backend.service.ports[0].name | string | `"http"` |  |
| spec.backend.service.ports[0].port | int | `80` |  |
| spec.backend.service.type | string | `"ClusterIP"` |  |
| spec.backend.serviceAccount.annotations | object | `{}` |  |
| spec.backend.serviceAccount.automountServiceAccountToken | bool | `true` |  |
| spec.backend.serviceAccount.create | bool | `false` |  |
| spec.backend.serviceAccount.name | string | `"maxai-agents-sa"` |  |
| spec.backend.tolerations | list | `[]` |  |
| spec.backend.topologySpreadConstraints | list | `[]` |  |
| spec.backend.volumeMounts.enabled | bool | `false` |  |
| spec.backend.volumes | list | `[]` |  |

## MaxAiParser parameters

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| spec.maxaiparser.affinity | list | `[]` |  |
| spec.maxaiparser.annotations | object | `{}` |  |
| spec.maxaiparser.configMap.data."tika-config.xml" | string | `"tikaConf: |\n  <properties>\n    <server>\n      <params>\n        <taskTimeoutMillis>1000000</taskTimeoutMillis>\n      </params>\n    </server>\n  </properties>\n"` |  |
| spec.maxaiparser.configMap.enabled | bool | `true` |  |
| spec.maxaiparser.deployment.enabled | bool | `true` |  |
| spec.maxaiparser.enabled | bool | `false` |  |
| spec.maxaiparser.hpa.apiVersion | string | `"autoscaling/v2"` |  |
| spec.maxaiparser.hpa.behavior | object | `{}` |  |
| spec.maxaiparser.hpa.enabled | bool | `false` |  |
| spec.maxaiparser.hpa.maxReplicaCount | int | `5` |  |
| spec.maxaiparser.hpa.metrics[0].resource.name | string | `"cpu"` |  |
| spec.maxaiparser.hpa.metrics[0].resource.target.averageUtilization | int | `80` |  |
| spec.maxaiparser.hpa.metrics[0].resource.target.type | string | `"Utilization"` |  |
| spec.maxaiparser.hpa.metrics[0].type | string | `"Resource"` |  |
| spec.maxaiparser.hpa.minReplicaCount | int | `0` |  |
| spec.maxaiparser.ingress.annotations | list | `[]` |  |
| spec.maxaiparser.ingress.className | string | `""` |  |
| spec.maxaiparser.ingress.enabled | bool | `false` |  |
| spec.maxaiparser.ingress.hosts | list | `[]` |  |
| spec.maxaiparser.ingress.tls | list | `[]` |  |
| spec.maxaiparser.labels | object | `{}` |  |
| spec.maxaiparser.livenessProbe.failureThreshold | int | `20` |  |
| spec.maxaiparser.livenessProbe.initialDelaySeconds | int | `15` |  |
| spec.maxaiparser.livenessProbe.periodSeconds | int | `5` |  |
| spec.maxaiparser.livenessProbe.scheme | string | `"HTTP"` |  |
| spec.maxaiparser.livenessProbe.timeoutSeconds | int | `30` |  |
| spec.maxaiparser.nodeSelector | object | `{}` |  |
| spec.maxaiparser.podAnnotations | object | `{}` |  |
| spec.maxaiparser.ports.containerPort | int | `80` |  |
| spec.maxaiparser.ports.protocol | string | `"http"` |  |
| spec.maxaiparser.priorityClassName | string | `nil` |  |
| spec.maxaiparser.readinessProbe.failureThreshold | int | `20` |  |
| spec.maxaiparser.readinessProbe.initialDelaySeconds | int | `15` |  |
| spec.maxaiparser.readinessProbe.periodSeconds | int | `5` |  |
| spec.maxaiparser.readinessProbe.scheme | string | `"HTTP"` |  |
| spec.maxaiparser.readinessProbe.timeoutSeconds | int | `30` |  |
| spec.maxaiparser.replicas | int | `1` |  |
| spec.maxaiparser.resources | object | `{}` |  |
| spec.maxaiparser.securityContexts.container.allowPrivilegeEscalation | bool | `true` |  |
| spec.maxaiparser.securityContexts.container.capabilities.drop[0] | string | `"ALL"` |  |
| spec.maxaiparser.securityContexts.container.readOnlyRootFilesystem | bool | `true` |  |
| spec.maxaiparser.securityContexts.container.runAsGroup | int | `35002` |  |
| spec.maxaiparser.securityContexts.container.runAsNonRoot | bool | `true` |  |
| spec.maxaiparser.securityContexts.container.runAsUser | int | `35002` |  |
| spec.maxaiparser.securityContexts.pod | object | `{}` |  |
| spec.maxaiparser.service.annotations | object | `{}` |  |
| spec.maxaiparser.service.ports[0].name | string | `"maxaiparser"` |  |
| spec.maxaiparser.service.ports[0].port | int | `9998` |  |
| spec.maxaiparser.service.type | string | `"ClusterIP"` |  |
| spec.maxaiparser.serviceAccount.annotations | object | `{}` |  |
| spec.maxaiparser.serviceAccount.automountServiceAccountToken | bool | `true` |  |
| spec.maxaiparser.serviceAccount.create | bool | `false` |  |
| spec.maxaiparser.serviceAccount.name | string | `nil` |  |
| spec.maxaiparser.startupProbe.failureThreshold | int | `6` |  |
| spec.maxaiparser.startupProbe.periodSeconds | int | `10` |  |
| spec.maxaiparser.startupProbe.scheme | string | `"HTTP"` |  |
| spec.maxaiparser.startupProbe.timeoutSeconds | int | `20` |  |
| spec.maxaiparser.tolerations | list | `[]` |  |
| spec.maxaiparser.topologySpreadConstraints | list | `[]` |  |


## Postgresql Parameters
| Key | Type | Default | Description |
|-----|------|---------|-------------|
| spec.postgresql.auth.database | string | `"maxaiagent"` |  |
| spec.postgresql.auth.existingSecret | string | `nil` |  |
| spec.postgresql.auth.password | string | `"maxaiagent"` |  |
| spec.postgresql.auth.postgresPassword | string | `"maxaiagent"` |  |
| spec.postgresql.auth.username | string | `"maxaiagent"` |  |
| spec.postgresql.enabled | bool | `true` |  |
| spec.postgresql.global.imagePullSecrets[0] | string | `"maxai-repo-secret"` |  |
| spec.postgresql.global.postgresql.auth.database | string | `"maxaiagent"` |  |
| spec.postgresql.global.postgresql.auth.existingSecret | string | `nil` |  |
| spec.postgresql.global.postgresql.auth.password | string | `"maxaiagent"` |  |
| spec.postgresql.global.postgresql.auth.postgresPassword | string | `"maxaiagent"` |  |
| spec.postgresql.global.postgresql.auth.username | string | `"maxaiagent"` |  |

## Redis Parameters
| Key | Type | Default | Description |
|-----|------|---------|-------------|
| spec.redis.auth.enabled | bool | `true` |  |
| spec.redis.auth.existingSecret | string | `""` |  |
| spec.redis.auth.existingSecretPasswordKey | string | `""` |  |
| spec.redis.auth.password | string | `"maxaiagent"` |  |
| spec.redis.auth.sentinel | bool | `true` |  |
| spec.redis.auth.usePasswordFiles | bool | `false` |  |
| spec.redis.enabled | bool | `false` |  |
| spec.redis.global.imagePullSecrets[0] | string | `"maxai-repo-secret"` |  |
| spec.redis.replica.replicaCount | int | `1` |  |


## UI Parameters
| Key | Type | Default | Description |
|-----|------|---------|-------------|
| spec.ui.affinity | list | `[]` |  |
| spec.ui.annotations | object | `{}` |  |
| spec.ui.args | list | `[]` |  |
| spec.ui.backend.backendPassword | string | `""` |  |
| spec.ui.backend.backendUser | string | `""` |  |
| spec.ui.backend.host | string | `"agent-01.max.local"` |  |
| spec.ui.backend.path | string | `"/fastapi"` |  |
| spec.ui.command | string | `nil` |  |
| spec.ui.configMap.enabled | bool | `false` |  |
| spec.ui.deployment.enabled | bool | `true` |  |
| spec.ui.enabled | bool | `false` |  |
| spec.ui.extraContainers | list | `[]` |  |
| spec.ui.hpa.apiVersion | string | `"autoscaling/v2"` |  |
| spec.ui.hpa.behavior | object | `{}` |  |
| spec.ui.hpa.enabled | bool | `false` |  |
| spec.ui.hpa.maxReplicaCount | int | `5` |  |
| spec.ui.hpa.metrics[0].resource.name | string | `"cpu"` |  |
| spec.ui.hpa.metrics[0].resource.target.averageUtilization | int | `80` |  |
| spec.ui.hpa.metrics[0].resource.target.type | string | `"Utilization"` |  |
| spec.ui.hpa.metrics[0].type | string | `"Resource"` |  |
| spec.ui.hpa.minReplicaCount | int | `0` |  |
| spec.ui.ingress.annotations | list | `[]` |  |
| spec.ui.ingress.className | string | `"nginx"` |  |
| spec.ui.ingress.enabled | bool | `true` |  |
| spec.ui.ingress.hosts[0].host | string | `"agent-01.max.local"` |  |
| spec.ui.ingress.hosts[0].paths[0].path | string | `"/"` |  |
| spec.ui.ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| spec.ui.ingress.tls[0].hosts[0] | string | `"agent-01.max.local"` |  |
| spec.ui.ingress.tls[0].secretName | string | `"agent-01-max-bknd-tls"` |  |
| spec.ui.initContainers | list | `[]` |  |
| spec.ui.livenessProbe.failureThreshold | int | `5` |  |
| spec.ui.livenessProbe.initialDelaySeconds | int | `15` |  |
| spec.ui.livenessProbe.periodSeconds | int | `10` |  |
| spec.ui.livenessProbe.scheme | string | `"HTTP"` |  |
| spec.ui.livenessProbe.timeoutSeconds | int | `5` |  |
| spec.ui.nodeSelector.nodegroup | string | `"spark"` |  |
| spec.ui.ports.containerPort | int | `80` |  |
| spec.ui.ports.protocol | string | `"http"` |  |
| spec.ui.priorityClassName | string | `nil` |  |
| spec.ui.readinessProbe.failureThreshold | int | `5` |  |
| spec.ui.readinessProbe.initialDelaySeconds | int | `15` |  |
| spec.ui.readinessProbe.periodSeconds | int | `10` |  |
| spec.ui.readinessProbe.scheme | string | `"HTTP"` |  |
| spec.ui.readinessProbe.timeoutSeconds | int | `5` |  |
| spec.ui.replicas | int | `1` |  |
| spec.ui.resources | object | `{}` |  |
| spec.ui.securityContext | object | `{}` |  |
| spec.ui.securityContexts.container | object | `{}` |  |
| spec.ui.securityContexts.pod | object | `{}` |  |
| spec.ui.service.annotations | object | `{}` |  |
| spec.ui.service.ports[0].name | string | `"http"` |  |
| spec.ui.service.ports[0].port | int | `80` |  |
| spec.ui.service.type | string | `"ClusterIP"` |  |
| spec.ui.serviceAccount.annotations | object | `{}` |  |
| spec.ui.serviceAccount.automountServiceAccountToken | bool | `true` |  |
| spec.ui.serviceAccount.create | bool | `false` |  |
| spec.ui.serviceAccount.name | string | `nil` |  |
| spec.ui.startupProbe.failureThreshold | int | `6` |  |
| spec.ui.startupProbe.periodSeconds | int | `10` |  |
| spec.ui.startupProbe.scheme | string | `"HTTP"` |  |
| spec.ui.startupProbe.timeoutSeconds | int | `20` |  |
| spec.ui.tolerations | list | `[]` |  |
| spec.ui.topologySpreadConstraints | list | `[]` |  |
