# alfresco-content-services

![Version: 7.0.0-SNAPSHOT](https://img.shields.io/badge/Version-7.0.0--SNAPSHOT-informational?style=flat-square) ![AppVersion: 23.1.0-A19](https://img.shields.io/badge/AppVersion-23.1.0--A19-informational?style=flat-square)

A Helm chart for deploying Alfresco Content Services

Please refer to the [documentation](https://github.com/Alfresco/acs-deployment/blob/master/docs/helm/README.md) for information on the Helm charts and deployment instructions.

**Homepage:** <https://www.alfresco.com>

## Source Code

* <https://github.com/Alfresco/acs-deployment>

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| https://activiti.github.io/activiti-cloud-helm-charts | alfresco-control-center(common) | 7.11.0 |
| https://activiti.github.io/activiti-cloud-helm-charts | alfresco-digital-workspace(common) | 7.11.0 |
| https://alfresco.github.io/alfresco-helm-charts/ | activemq | 3.1.0 |
| https://alfresco.github.io/alfresco-helm-charts/ | alfresco-common | 2.1.0-alpha.2 |
| https://alfresco.github.io/alfresco-helm-charts/ | alfresco-connector-msteams | 0.1.0 |
| https://alfresco.github.io/alfresco-helm-charts/ | alfresco-search-enterprise | 1.3.0 |
| https://alfresco.github.io/alfresco-helm-charts/ | alfresco-search(alfresco-search-service) | 1.2.0 |
| https://alfresco.github.io/alfresco-helm-charts/ | share(alfresco-share) | 0.1.0-alpha.2 |
| https://alfresco.github.io/alfresco-helm-charts/ | alfresco-sync-service | 4.2.0 |
| https://alfresco.github.io/alfresco-helm-charts/ | alfresco-transform-service | 0.1.1 |
| oci://registry-1.docker.io/bitnamicharts | postgresql | 12.5.6 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| activemq.adminUser.existingSecretName | string | `"acs-alfresco-cs-brokersecret"` |  |
| activemq.adminUser.password | string | `"admin"` | Default password for the embedded broker admin user |
| activemq.adminUser.user | string | `"admin"` | Default username for the embedded broker admin user |
| activemq.enabled | bool | `true` |  |
| activemq.existingSecretName | string | `nil` |  |
| activemq.nameOverride | string | `"activemq"` |  |
| activemq.nodeSelector | object | `{}` | Possibility to choose Node for pod, with a key-value pair label e.g {"kubernetes.io/hostname": multinode-demo-m02} |
| aiTransformer.environment.JAVA_OPTS | string | `"-XX:MinRAMPercentage=50 -XX:MaxRAMPercentage=80"` |  |
| aiTransformer.image.internalPort | int | `8090` |  |
| aiTransformer.image.pullPolicy | string | `"IfNotPresent"` |  |
| aiTransformer.image.repository | string | `"quay.io/alfresco/alfresco-ai-docker-engine"` |  |
| aiTransformer.image.tag | string | `"2.0.0"` |  |
| aiTransformer.livenessProbe.initialDelaySeconds | int | `10` |  |
| aiTransformer.livenessProbe.livenessPercent | int | `400` |  |
| aiTransformer.livenessProbe.livenessTransformPeriodSeconds | int | `600` |  |
| aiTransformer.livenessProbe.maxTransformSeconds | int | `1800` |  |
| aiTransformer.livenessProbe.maxTransforms | int | `10000` |  |
| aiTransformer.livenessProbe.periodSeconds | int | `20` |  |
| aiTransformer.livenessProbe.timeoutSeconds | int | `10` |  |
| aiTransformer.nodeSelector | object | `{}` |  |
| aiTransformer.podSecurityContext.runAsUser | int | `33015` |  |
| aiTransformer.readinessProbe.initialDelaySeconds | int | `20` |  |
| aiTransformer.readinessProbe.periodSeconds | int | `60` |  |
| aiTransformer.readinessProbe.timeoutSeconds | int | `10` |  |
| aiTransformer.replicaCount | int | `2` |  |
| aiTransformer.resources.limits.cpu | string | `"2"` |  |
| aiTransformer.resources.limits.memory | string | `"1Gi"` |  |
| aiTransformer.resources.requests.cpu | string | `"50m"` |  |
| aiTransformer.resources.requests.memory | string | `"200Mi"` |  |
| aiTransformer.service.externalPort | int | `80` |  |
| aiTransformer.service.name | string | `"ai-transformer"` |  |
| aiTransformer.service.type | string | `"ClusterIP"` |  |
| alfresco-connector-msteams.enabled | bool | `false` | Enable/Disable Alfresco Content Connector for Microsoft Teams |
| alfresco-connector-msteams.image.repository | string | `"quay.io/alfresco/alfresco-ms-teams-service"` |  |
| alfresco-connector-msteams.image.tag | string | `"2.0.0"` |  |
| alfresco-control-center.enabled | bool | `true` |  |
| alfresco-control-center.env.API_URL | string | `"{protocol}//{hostname}{:port}"` |  |
| alfresco-control-center.env.APP_CONFIG_AUTH_TYPE | string | `"BASIC"` |  |
| alfresco-control-center.env.APP_CONFIG_PROVIDER | string | `"ECM"` |  |
| alfresco-control-center.image.pullPolicy | string | `"IfNotPresent"` |  |
| alfresco-control-center.image.repository | string | `"quay.io/alfresco/alfresco-control-center"` |  |
| alfresco-control-center.image.tag | string | `"8.1.0-5421573582"` |  |
| alfresco-control-center.ingress.annotations."kubernetes.io/ingress.class" | string | `"nginx"` |  |
| alfresco-control-center.ingress.path | string | `"/control-center"` |  |
| alfresco-control-center.ingress.tls | list | `[]` |  |
| alfresco-control-center.nameOverride | string | `"alfresco-cc"` |  |
| alfresco-control-center.nodeSelector | object | `{}` |  |
| alfresco-control-center.resources.limits.cpu | string | `"1"` |  |
| alfresco-control-center.resources.limits.memory | string | `"1024Mi"` |  |
| alfresco-control-center.resources.requests.cpu | string | `"0.25"` |  |
| alfresco-control-center.resources.requests.memory | string | `"256Mi"` |  |
| alfresco-control-center.securityContext.capabilities.drop[0] | string | `"NET_RAW"` |  |
| alfresco-control-center.securityContext.capabilities.drop[1] | string | `"ALL"` |  |
| alfresco-control-center.securityContext.runAsNonRoot | bool | `true` |  |
| alfresco-control-center.securityContext.runAsUser | int | `101` |  |
| alfresco-control-center.service.envType | string | `"frontend"` |  |
| alfresco-digital-workspace.enabled | bool | `true` |  |
| alfresco-digital-workspace.env.API_URL | string | `"{protocol}//{hostname}{:port}"` |  |
| alfresco-digital-workspace.env.APP_CONFIG_AUTH_TYPE | string | `"BASIC"` |  |
| alfresco-digital-workspace.env.APP_CONFIG_PROVIDER | string | `"ECM"` |  |
| alfresco-digital-workspace.extraEnv | string | `"{{- if .Values.global.ai.enabled }}\n- name: APP_CONFIG_PLUGIN_AI_SERVICE\n  value: '{{ .Values.global.ai.enabled }}'\n{{- end }}"` |  |
| alfresco-digital-workspace.image.pullPolicy | string | `"IfNotPresent"` |  |
| alfresco-digital-workspace.image.repository | string | `"quay.io/alfresco/alfresco-digital-workspace"` |  |
| alfresco-digital-workspace.image.tag | string | `"4.1.0-5421573582"` |  |
| alfresco-digital-workspace.ingress.annotations."kubernetes.io/ingress.class" | string | `"nginx"` |  |
| alfresco-digital-workspace.ingress.annotations."nginx.ingress.kubernetes.io/proxy-body-size" | string | `"5g"` |  |
| alfresco-digital-workspace.ingress.path | string | `"/workspace"` |  |
| alfresco-digital-workspace.ingress.tls | list | `[]` |  |
| alfresco-digital-workspace.nameOverride | string | `"alfresco-dw"` |  |
| alfresco-digital-workspace.nodeSelector | object | `{}` |  |
| alfresco-digital-workspace.resources.limits.cpu | string | `"1"` |  |
| alfresco-digital-workspace.resources.limits.memory | string | `"1024Mi"` |  |
| alfresco-digital-workspace.resources.requests.cpu | string | `"0.25"` |  |
| alfresco-digital-workspace.resources.requests.memory | string | `"256Mi"` |  |
| alfresco-digital-workspace.securityContext.capabilities.drop[0] | string | `"NET_RAW"` |  |
| alfresco-digital-workspace.securityContext.capabilities.drop[1] | string | `"ALL"` |  |
| alfresco-digital-workspace.securityContext.runAsNonRoot | bool | `true` |  |
| alfresco-digital-workspace.securityContext.runAsUser | int | `101` |  |
| alfresco-digital-workspace.service.envType | string | `"frontend"` |  |
| alfresco-search-enterprise.elasticsearch.enabled | bool | `true` | Enables the embedded elasticsearch cluster |
| alfresco-search-enterprise.enabled | bool | `false` |  |
| alfresco-search-enterprise.liveIndexing.content.image.tag | string | `"3.4.0-M1"` |  |
| alfresco-search-enterprise.liveIndexing.mediation.image.tag | string | `"3.4.0-M1"` |  |
| alfresco-search-enterprise.liveIndexing.metadata.image.tag | string | `"3.4.0-M1"` |  |
| alfresco-search-enterprise.liveIndexing.path.image.tag | string | `"3.4.0-M1"` |  |
| alfresco-search-enterprise.messageBroker.existingSecretName | string | `"acs-alfresco-cs-brokersecret"` |  |
| alfresco-search-enterprise.reindexing.enabled | bool | `true` |  |
| alfresco-search-enterprise.reindexing.image.tag | string | `"3.4.0-M1"` |  |
| alfresco-search-enterprise.reindexing.postgresql.database | string | `"alfresco"` |  |
| alfresco-search-enterprise.reindexing.postgresql.existingSecretName | string | `"acs-alfresco-cs-dbsecret"` |  |
| alfresco-search-enterprise.reindexing.postgresql.hostname | string | `"postgresql-acs"` |  |
| alfresco-search-enterprise.reindexing.postgresql.url | string | `nil` |  |
| alfresco-search.alfresco-insight-zeppelin.enabled | bool | `false` |  |
| alfresco-search.enabled | bool | `true` |  |
| alfresco-search.external.host | string | `nil` | Host dns/ip of the external solr6 instance. |
| alfresco-search.external.port | string | `nil` | Port of the external solr6 instance. |
| alfresco-search.ingress.basicAuth | string | `nil` | Default solr basic auth user/password: admin / admin You can create your own with htpasswd utilility & encode it with base64. Example: `echo -n "$(htpasswd -nbm admin admin)" | base64 | tr -d '\n'` basicAuth: YWRtaW46JGFwcjEkVVJqb29uS00kSEMuS1EwVkRScFpwSHB2a3JwTDd1Lg== |
| alfresco-search.ingress.enabled | bool | `false` | Alfresco Search services endpoint ('/solr') |
| alfresco-search.ingress.tls | list | `[]` |  |
| alfresco-search.nameOverride | string | `"alfresco-search"` |  |
| alfresco-search.searchServicesImage.repository | string | `"quay.io/alfresco/search-services"` |  |
| alfresco-search.searchServicesImage.tag | string | `"2.0.8-A1"` |  |
| alfresco-sync-service.enabled | bool | `true` | Toggle deployment of Alfresco Sync Service (Desktop-Sync) Check [Alfresco Sync Service Documentation](https://github.com/Alfresco/alfresco-helm-charts/tree/main/charts/alfresco-sync-service) |
| alfresco-sync-service.image.tag | string | `"4.0.0-M9"` |  |
| alfresco-sync-service.messageBroker.existingSecretName | string | `"acs-alfresco-cs-brokersecret"` |  |
| alfresco-sync-service.postgresql.auth.database | string | `"syncservice-postgresql"` |  |
| alfresco-sync-service.postgresql.auth.enablePostgresUser | bool | `false` |  |
| alfresco-sync-service.postgresql.auth.password | string | `"admin"` |  |
| alfresco-sync-service.postgresql.auth.username | string | `"alfresco"` |  |
| alfresco-sync-service.postgresql.enabled | bool | `true` |  |
| alfresco-sync-service.postgresql.image.tag | string | `"14.4.0"` |  |
| alfresco-sync-service.postgresql.primary.resources.limits.cpu | string | `"4"` |  |
| alfresco-sync-service.postgresql.primary.resources.limits.memory | string | `"4Gi"` |  |
| alfresco-sync-service.postgresql.primary.resources.requests.cpu | string | `"250m"` |  |
| alfresco-sync-service.postgresql.primary.resources.requests.memory | string | `"1Gi"` |  |
| alfresco-sync-service.repository.nameOverride | string | `"alfresco-cs-repository"` |  |
| alfresco-sync-service.repository.port | int | `80` |  |
| alfresco-transform-service.aiTransformer.environment.JAVA_OPTS | string | `"-XX:MinRAMPercentage=50 -XX:MaxRAMPercentage=80"` |  |
| alfresco-transform-service.aiTransformer.image.internalPort | int | `8090` |  |
| alfresco-transform-service.aiTransformer.image.pullPolicy | string | `"IfNotPresent"` |  |
| alfresco-transform-service.aiTransformer.image.repository | string | `"quay.io/alfresco/alfresco-ai-docker-engine"` |  |
| alfresco-transform-service.aiTransformer.image.tag | string | `"2.0.0"` |  |
| alfresco-transform-service.aiTransformer.livenessProbe.initialDelaySeconds | int | `10` |  |
| alfresco-transform-service.aiTransformer.livenessProbe.livenessPercent | int | `400` |  |
| alfresco-transform-service.aiTransformer.livenessProbe.livenessTransformPeriodSeconds | int | `600` |  |
| alfresco-transform-service.aiTransformer.livenessProbe.maxTransformSeconds | int | `1800` |  |
| alfresco-transform-service.aiTransformer.livenessProbe.maxTransforms | int | `10000` |  |
| alfresco-transform-service.aiTransformer.livenessProbe.periodSeconds | int | `20` |  |
| alfresco-transform-service.aiTransformer.livenessProbe.timeoutSeconds | int | `10` |  |
| alfresco-transform-service.aiTransformer.nodeSelector | object | `{}` |  |
| alfresco-transform-service.aiTransformer.podSecurityContext.runAsUser | int | `33015` |  |
| alfresco-transform-service.aiTransformer.readinessProbe.initialDelaySeconds | int | `20` |  |
| alfresco-transform-service.aiTransformer.readinessProbe.periodSeconds | int | `60` |  |
| alfresco-transform-service.aiTransformer.readinessProbe.timeoutSeconds | int | `10` |  |
| alfresco-transform-service.aiTransformer.replicaCount | int | `2` |  |
| alfresco-transform-service.aiTransformer.resources.limits.cpu | string | `"2"` |  |
| alfresco-transform-service.aiTransformer.resources.limits.memory | string | `"1Gi"` |  |
| alfresco-transform-service.aiTransformer.resources.requests.cpu | string | `"50m"` |  |
| alfresco-transform-service.aiTransformer.resources.requests.memory | string | `"200Mi"` |  |
| alfresco-transform-service.aiTransformer.service.externalPort | int | `80` |  |
| alfresco-transform-service.aiTransformer.service.name | string | `"ai-transformer"` |  |
| alfresco-transform-service.aiTransformer.service.type | string | `"ClusterIP"` |  |
| alfresco-transform-service.enabled | bool | `true` |  |
| alfresco-transform-service.filestore | object | `{"image":{"repository":"quay.io/alfresco/alfresco-shared-file-store","tag":"3.0.0"},"persistence":{"data":{"mountPath":"/tmp/Alfresco","subPath":"alfresco-content-services/filestore-data"},"enabled":true},"replicaCount":1}` | Deprecated, use alfresco-transform-service.filestore instead |
| alfresco-transform-service.filestore.persistence.enabled | bool | `true` | Persist filestore data |
| alfresco-transform-service.imagemagick | object | `{"image":{"repository":"alfresco/alfresco-imagemagick","tag":"4.0.0"}}` | Deprecated, use alfresco-transform-service.imagemagick instead |
| alfresco-transform-service.libreoffice | object | `{"image":{"repository":"alfresco/alfresco-libreoffice","tag":"4.0.0"}}` | Deprecated, use alfresco-transform-service.libreoffice instead |
| alfresco-transform-service.messageBroker.existingSecretName | string | `"acs-alfresco-cs-brokersecret"` |  |
| alfresco-transform-service.pdfrenderer | object | `{"image":{"repository":"alfresco/alfresco-pdf-renderer","tag":"4.0.0"}}` | Deprecated, use alfresco-transform-service.pdfrenderer instead |
| alfresco-transform-service.tika | object | `{"image":{"repository":"alfresco/alfresco-tika","tag":"4.0.0"}}` | Deprecated, use alfresco-transform-service.tika instead |
| alfresco-transform-service.transformmisc | object | `{"image":{"repository":"alfresco/alfresco-transform-misc","tag":"4.0.0"}}` | Deprecated, use alfresco-transform-service.transformmisc instead |
| alfresco-transform-service.transformrouter.image.repository | string | `"quay.io/alfresco/alfresco-transform-router"` |  |
| alfresco-transform-service.transformrouter.image.tag | string | `"3.0.0"` |  |
| alfresco-transform-service.transformrouter.replicaCount | int | `2` |  |
| apiexplorer | object | `{"ingress":{"path":"/api-explorer"}}` | Declares the api-explorer service used by the content repository |
| database.driver | string | `nil` | Postgresql jdbc driver name ex: org.postgresql.Driver. It should be available in the container image. |
| database.existingSecretName | string | `nil` | An existing secret that contains DATABASE_USERNAME and DATABASE_PASSWORD keys. When using embedded postgres you need to also set `postgresql.existingSecret`. |
| database.external | bool | `false` | Enable using an external database for Alfresco Content Services. Must disable `postgresql.enabled` when true. |
| database.password | string | `nil` | External Postgresql database password |
| database.secretName | string | `"acs-alfresco-cs-dbsecret"` | Name of the secret managed by this chart |
| database.url | string | `nil` | External Postgresql jdbc url ex: `jdbc:postgresql://oldfashioned-mule-postgresql-acs:5432/alfresco` |
| database.user | string | `nil` | External Postgresql database user |
| email | object | `{"handler":{"folder":{"overwriteDuplicates":true}},"inbound":{"emailContributorsAuthority":"EMAIL_CONTRIBUTORS","enabled":false,"unknownUser":"anonymous"},"initContainers":{"pemToKeystore":{"image":{"pullPolicy":"IfNotPresent","repository":"registry.access.redhat.com/redhat-sso-7/sso71-openshift","tag":"1.1-16"}},"pemToTruststore":{"image":{"pullPolicy":"IfNotPresent","repository":"registry.access.redhat.com/redhat-sso-7/sso71-openshift","tag":"1.1-16"}},"setPerms":{"image":{"pullPolicy":"IfNotPresent","repository":"busybox","tag":"1.35.0"}}},"server":{"allowed":{"senders":".*"},"auth":{"enabled":true},"blocked":{"senders":null},"connections":{"max":3},"domain":null,"enableTLS":true,"enabled":false,"hideTLS":false,"port":1125,"requireTLS":false},"ssl":{"secretName":null}}` | For a full information of configuring the inbound email system, see https://docs.alfresco.com/content-services/latest/config/email/#manage-inbound-emails |
| filestore | object | `{"image":{"repository":"quay.io/alfresco/alfresco-shared-file-store","tag":"3.0.0"},"persistence":{"data":{"mountPath":"/tmp/Alfresco","subPath":"alfresco-content-services/filestore-data"},"enabled":true},"replicaCount":1}` | Declares the alfresco-shared-file-store used by the content repository and transform service |
| filestore.persistence.enabled | bool | `true` | Persist filestore data |
| global.ai | object | `{"enabled":false}` | Choose if you want AI capabilities (globally - including ADW AI plugin) |
| global.alfrescoRegistryPullSecrets | string | `nil` | If a private image registry a secret can be defined and passed to kubernetes, see: https://github.com/Alfresco/acs-deployment/blob/a924ad6670911f64f1bba680682d266dd4ea27fb/docs/helm/eks-deployment.md#docker-registry-secret |
| global.elasticsearch | object | `{"host":"elasticsearch-master","password":null,"port":9200,"protocol":"http","user":null}` | Shared connections details for Elasticsearch/Opensearch, required when alfresco-search-enterprise.enabled is true |
| global.elasticsearch.host | string | `"elasticsearch-master"` | The host where service is available. The provided default is for when elasticsearch.enabled is true |
| global.elasticsearch.password | string | `nil` | The password required to access the service, if any |
| global.elasticsearch.port | int | `9200` | The port where service is available |
| global.elasticsearch.protocol | string | `"http"` | Valid values are http or https |
| global.elasticsearch.user | string | `nil` | The username required to access the service, if any |
| global.known_urls[0] | string | `"https://localhost"` |  |
| global.known_urls[1] | string | `"http://localhost"` |  |
| global.registryPullSecrets[0] | string | `"quay-registry-secret"` |  |
| global.strategy.rollingUpdate.maxSurge | int | `1` |  |
| global.strategy.rollingUpdate.maxUnavailable | int | `0` |  |
| global.tracking.auth | string | `"secret"` | Select how solr and repo authenticate to each other none: work only prior to acs 7.2 (and was the default) secret: use a shared secret (to specify using `tracking.sharedsecret`) https: to use mTLS auth (require appropriate certificate configuration) |
| global.tracking.sharedsecret | string | `nil` | Shared secret to authenticate repo/solr traffic. Strong enough secret can be generated with `openssl rand 20 -base64` |
| imagemagick | object | `{"image":{"repository":"alfresco/alfresco-imagemagick","tag":"4.0.0"}}` | Declares the alfresco-imagemagick service used by the content repository to transform image files |
| imap | object | `{"mail":{"from":{"default":null},"to":{"default":null}},"server":{"enabled":false,"host":"0.0.0.0","imap":{"enabled":true},"imaps":{"enabled":true,"port":1144},"port":1143}}` | For a full information of configuring the imap subsystem, see https://docs.alfresco.com/content-services/latest/config/email/#enable-imap-protocol-using-alfresco-globalproperties |
| libreoffice | object | `{"image":{"repository":"alfresco/alfresco-libreoffice","tag":"4.0.0"}}` | Declares the alfresco-libreoffice service used by the content repository to transform office files |
| mail | object | `{"encoding":"UTF-8","existingSecretName":null,"from":{"default":null,"enabled":false},"host":null,"password":null,"port":25,"protocol":"smtps","smtp":{"auth":true,"debug":false,"starttls":{"enable":true},"timeout":30000},"smtps":{"auth":true,"starttls":{"enable":true}},"username":null}` | For a full information of configuring the outbound email system, see https://docs.alfresco.com/content-services/latest/config/email/#manage-outbound-emails |
| mail.existingSecretName | string | `nil` | An existing kubernetes secret that contains MAIL_PASSWORD as per `mail.password` value |
| mail.from.default | string | `nil` | Specifies the email address from which email notifications are sent |
| mail.host | string | `nil` | SMTP(S) host server to enable delivery of site invitations, activity notifications and workflow tasks by email |
| messageBroker | object | `{"password":null,"secretName":"acs-alfresco-cs-brokersecret","url":null,"user":null}` | Activemq connection setting when activemq.enabled=false Can reference an external broker details, or help spread details of an internal one. |
| messageBroker.secretName | string | `"acs-alfresco-cs-brokersecret"` | Name of the secret managed by this chart |
| metadataKeystore.defaultKeyPassword | string | `"oKIWzVdEdA"` |  |
| metadataKeystore.defaultKeystorePassword | string | `"mp6yc0UD9e"` |  |
| ooi | object | `{"enabled":false}` | Enable/Disable Alfresco Collaboration Connector for Microsoft 365 |
| ooiService.environment.JAVA_OPTS | string | `" -Dalfresco.base-url=http://acs-alfresco-cs-repository:80"` |  |
| ooiService.image.internalPort | int | `9095` |  |
| ooiService.image.pullPolicy | string | `"IfNotPresent"` |  |
| ooiService.image.repository | string | `"quay.io/alfresco/alfresco-ooi-service"` |  |
| ooiService.image.tag | string | `"2.0.0"` |  |
| ooiService.ingress.path | string | `"/ooi-service"` |  |
| ooiService.ingress.tls | list | `[]` |  |
| ooiService.livenessProbe.initialDelaySeconds | int | `10` |  |
| ooiService.livenessProbe.periodSeconds | int | `20` |  |
| ooiService.livenessProbe.timeoutSeconds | int | `10` |  |
| ooiService.nodeSelector | object | `{}` |  |
| ooiService.podSecurityContext.runAsNonRoot | bool | `true` |  |
| ooiService.podSecurityContext.runAsUser | int | `33006` |  |
| ooiService.readinessProbe.initialDelaySeconds | int | `20` |  |
| ooiService.readinessProbe.periodSeconds | int | `60` |  |
| ooiService.readinessProbe.timeoutSeconds | int | `10` |  |
| ooiService.replicaCount | int | `2` |  |
| ooiService.resources.limits.cpu | string | `"2"` |  |
| ooiService.resources.limits.memory | string | `"2Gi"` |  |
| ooiService.resources.requests.cpu | string | `"50m"` |  |
| ooiService.resources.requests.memory | string | `"200Mi"` |  |
| ooiService.service.externalPort | int | `80` |  |
| ooiService.service.name | string | `"ooi-service"` |  |
| ooiService.service.type | string | `"ClusterIP"` |  |
| pdfrenderer | object | `{"image":{"repository":"alfresco/alfresco-pdf-renderer","tag":"4.0.0"}}` | Declares the alfresco-pdf-renderer service used by the content repository to transform pdf files |
| postgresql.auth.database | string | `"alfresco"` |  |
| postgresql.auth.existingSecret | string | `nil` |  |
| postgresql.auth.password | string | `"alfresco"` |  |
| postgresql.auth.username | string | `"alfresco"` |  |
| postgresql.commonAnnotations.application | string | `"alfresco-content-services"` |  |
| postgresql.enabled | bool | `true` | Toggle embedded postgres for Alfresco Content Services repository Check [PostgreSQL Bitnami chart Documentation](https://github.com/bitnami/charts/tree/main/bitnami/postgresql) |
| postgresql.image.pullPolicy | string | `"IfNotPresent"` |  |
| postgresql.image.tag | string | `"14.4.0"` |  |
| postgresql.nameOverride | string | `"postgresql-acs"` |  |
| postgresql.primary.extendedConfiguration | string | `"max_connections = 250\nshared_buffers = 512MB\neffective_cache_size = 2GB\nwal_level = minimal\nmax_wal_senders = 0\nmax_replication_slots = 0\nlog_min_messages = LOG\n"` |  |
| postgresql.primary.persistence.existingClaim | string | `nil` | provide an existing persistent volume claim name to persist SQL data Make sure the root folder has the appropriate permissions/ownhership set. |
| postgresql.primary.persistence.storageClass | string | `nil` | set the storageClass to use for dynamic provisioning. setting it to null means "default storageClass". |
| postgresql.primary.persistence.subPath | string | `"alfresco-content-services/database-data"` |  |
| postgresql.primary.resources.limits.cpu | string | `"8"` |  |
| postgresql.primary.resources.limits.memory | string | `"8Gi"` |  |
| postgresql.primary.resources.requests.cpu | string | `"500m"` |  |
| postgresql.primary.resources.requests.memory | string | `"1Gi"` |  |
| repository.adminPassword | string | `"209c6174da490caeb422f3fa5a7ae634"` | Administrator password for ACS in NTLM hash format to set at bootstrap time |
| repository.command | list | `[]` |  |
| repository.edition | string | `"Enterprise"` |  |
| repository.environment.JAVA_OPTS | string | `"-XX:MinRAMPercentage=50 -XX:MaxRAMPercentage=80 -Dencryption.keystore.type=JCEKS -Dencryption.cipherAlgorithm=DESede/CBC/PKCS5Padding -Dencryption.keyAlgorithm=DESede -Dencryption.keystore.location=/usr/local/tomcat/shared/classes/alfresco/extension/keystore/keystore -Dmetadata-keystore.aliases=metadata -Dmetadata-keystore.metadata.algorithm=DESede"` |  |
| repository.existingSecretName | string | `nil` | An existing secret that contains REPO_ADMIN_PASSWORD as an alternative for `repository.adminPassword` value |
| repository.extraInitContainers | list | `[]` |  |
| repository.extraLogStatements | object | `{}` | Provide additional log statements by adding classes and/or packages in a key:value maner org.alfresco.repo.content.transform.TransformerDebug: debug |
| repository.extraSideContainers | list | `[]` |  |
| repository.extraVolumeMounts | list | `[]` |  |
| repository.extraVolumes | list | `[]` |  |
| repository.image.hazelcastPort | int | `5701` |  |
| repository.image.internalPort | int | `8080` |  |
| repository.image.pullPolicy | string | `"IfNotPresent"` |  |
| repository.image.repository | string | `"quay.io/alfresco/alfresco-content-repository"` |  |
| repository.image.tag | string | `"23.1.0-A19"` |  |
| repository.ingress.annotations | object | `{}` |  |
| repository.ingress.maxUploadSize | string | `"5g"` |  |
| repository.ingress.path | string | `"/"` |  |
| repository.ingress.tls | list | `[]` |  |
| repository.initContainers.db.image.pullPolicy | string | `"IfNotPresent"` |  |
| repository.initContainers.db.image.repository | string | `"busybox"` |  |
| repository.initContainers.db.image.tag | string | `"1.35.0"` |  |
| repository.initContainers.db.resources.limits.cpu | string | `"0.25"` |  |
| repository.initContainers.db.resources.limits.memory | string | `"10Mi"` |  |
| repository.licenseSecret | string | `nil` | The name of the secret holding the ACS repository license if any. it must be contained within a `data['*.lic']` property For details on how to manage license, see: https://github.com/Alfresco/acs-deployment/blob/master/docs/helm/examples/alf_license.md |
| repository.livenessProbe.initialDelaySeconds | int | `130` |  |
| repository.livenessProbe.periodSeconds | int | `20` |  |
| repository.livenessProbe.timeoutSeconds | int | `10` |  |
| repository.nodeSelector | object | `{}` |  |
| repository.persistence.accessModes | list | `["ReadWriteMany"]` | Specify a storageClass for dynamic provisioning |
| repository.persistence.baseSize | string | `"20Gi"` |  |
| repository.persistence.data.mountPath | string | `"/usr/local/tomcat/alf_data"` |  |
| repository.persistence.data.subPath | string | `"alfresco-content-services/repository-data"` |  |
| repository.persistence.enabled | bool | `true` | Persist repository data |
| repository.persistence.existingClaim | string | `nil` | Use pre-provisioned pv through its claim (e.g. static provisioning) |
| repository.persistence.storageClass | string | `nil` | Bind PVC based on storageClass (e.g. dynamic provisioning) |
| repository.podSecurityContext.fsGroup | int | `1000` |  |
| repository.podSecurityContext.runAsGroup | int | `1000` |  |
| repository.podSecurityContext.runAsNonRoot | bool | `true` |  |
| repository.podSecurityContext.runAsUser | int | `33000` |  |
| repository.readinessProbe.failureThreshold | int | `6` |  |
| repository.readinessProbe.initialDelaySeconds | int | `60` |  |
| repository.readinessProbe.periodSeconds | int | `20` |  |
| repository.readinessProbe.timeoutSeconds | int | `10` |  |
| repository.replicaCount | int | `2` |  |
| repository.resources.limits.cpu | string | `"4"` |  |
| repository.resources.limits.memory | string | `"8Gi"` |  |
| repository.resources.requests.cpu | string | `"250m"` |  |
| repository.resources.requests.memory | string | `"2Gi"` |  |
| repository.service.externalPort | int | `80` |  |
| repository.service.name | string | `"alfresco"` |  |
| repository.service.type | string | `"ClusterIP"` |  |
| repository.startupProbe | object | `{"failureThreshold":10,"periodSeconds":30}` | The startup probe to cover the worse case startup time for slow clusters |
| repository.strategy.type | string | `"Recreate"` |  |
| s3connector.config.bucketLocation | string | `nil` |  |
| s3connector.config.bucketName | string | `nil` |  |
| s3connector.enabled | bool | `false` | Enable the S3 Connector For a full list of properties on the S3 connector see: https://docs.alfresco.com/s3connector/references/s3-contentstore-ref-config-props.html |
| s3connector.existingSecretName | string | `nil` | An existing kubernetes secret that contains ACCESSKEY, SECRETKEY, ENCRYPTION, KMSKEYID keys |
| s3connector.secrets.accessKey | string | `nil` |  |
| s3connector.secrets.awsKmsKeyId | string | `nil` |  |
| s3connector.secrets.encryption | string | `nil` |  |
| s3connector.secrets.secretKey | string | `nil` |  |
| share.enabled | bool | `true` | toggle deplying Alfresco Share UI |
| share.image.repository | string | `"quay.io/alfresco/alfresco-share"` |  |
| share.image.tag | string | `"23.1.0-A19"` |  |
| share.nameOverride | string | `"share"` |  |
| share.repository.existingConfigMap.keys.host | string | `"repo_svc_name"` | Name of the key in the configmap which points to the repository service hostname |
| share.repository.existingConfigMap.keys.port | string | `"repo_svc_port"` | Name of the key in the configmap which points to the repository service port |
| share.repository.existingConfigMap.name | string | `"infrastructure-repository"` | Name of the configmap which hold the repositoy connection details |
| tika | object | `{"image":{"repository":"alfresco/alfresco-tika","tag":"4.0.0"}}` | Declares the alfresco-tika service used by the content repository to transform office files |
| transformmisc | object | `{"image":{"repository":"alfresco/alfresco-transform-misc","tag":"4.0.0"}}` | Declares the alfresco-tika service used by the content repository to transform office files |
| transformrouter | object | `{"image":{"repository":"quay.io/alfresco/alfresco-transform-router","tag":"3.0.0"},"replicaCount":2}` | Declares the alfresco-transform-router service used by the content repository to route transformation requests |

Alfresco Content Service will be deployed in a Kubernetes cluster. This cluster
needs a at least 32GB memory to split among below pods:

* 2 x repository
* 1 x share
* 1 x search
* 2 x pdfrenderer
* 2 x imagemagick
* 2 libreoffice
* 2 tika
* 2 misc
* 1 x postgresql
* 1 activemq

> Note: this is the default settings but requirements can be lowered by
dropping the `replicaCount` value to 1 for each service.

Default CPU and memory requirements for each pods are set as low as e think is
reasonable. If you need to teak the resource allocation you can use the
`resources.limits.cpu` & `resources.limits.memory` for each component of the
platform. Remember that most of them are running in JAVA VM so you might want
to also raise the JVM memory settings (-Xmx) which is possible using pods'
environment variables.
