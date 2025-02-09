# Upgrading the helm charts

Our helm charts are continuously improved and sometimes arise the need to
introduce a breaking change.

To get an overview of the changes in each release, first take a look at the
release notes that are available via [GitHub Releases](https://github.com/Alfresco/acs-deployment/releases).

Here follows a more detailed explanation of any breaking change grouped by
version in which they have been released.

## To be released (likely 7.0.0)

Due to breaking changes the next version will be a major release.

### MSTeams chart rename

The previous `ms-teams-service` subchart has been renamed to
`alfresco-connector-msteams` to better reflect the product name during the
migration to the new
[alfresco-helm-charts](https://github.com/Alfresco/alfresco-helm-charts)
repository.

Accordingly to this chart rename, also the related values has been moved from
`.Values.msTeamsService` to
`.Values.alfresco-connector-msteams`.

### externalHost, externalPort & externalProtocol are not used anymore

In previous versions of the charts one could use the values below to tell the
charts how to configure Alfresco repo & Share, specifically for security
features (CSRF, CORS):

* `externalHost`
* `externalPort`
* `externalProtocol`

These were simple strings and did not allow for multiple domains/URLs to be
used which is exactly one would be expect to do when configuring cross-origin
protections.
This is now possible as we introduce the newer `known_urls` value.
This value can be either passed to share or repo directly or set in the global
context. Being able to use either the subchart or the global context Allows for
conveniently set this parameter at once for all subcharts or on the contrary
use different values different subcharts if they do not trust the same
domains/URLs.

Global setting:

```yaml
global:
  known_urls:
    - https://ecm.domain.tld
    - http://app.domain.local:8080/crm
```

Targeted setting:

```yaml
share:
  known_urls:
    - https://ecm.domain.tld
repository:
  known_urls:
    - https://ecm.domain.tld
    - http://app.domain.local:8080/crm
```

**The first item in the list will be considered the main domain where alfresco
& Share are installed**

If you want to use the `--set` switch of the `helm` command`, you can still do
it by using either of the syntaxes below to pass a list:

Comma separated list (commas must be escaped):

```bash
helm install alfresco-content-services acs --set global.known_urls=https://ecm.domain.tld\,http://app.domain.local:8080/crm
```

Indexed syntax square brackets must be escaped:

```bash
helm install alfresco-content-services acs \
  --set global.known_urls\[0\]=https://ecm.domain.tld
  --set global.known_urls\[1\]=http://app.domain.local:8080/crm
```

> Note: We would encorage you to avoid using `--set` as much as possible and
> use `--values` instead with values stored in yaml files.

### Alfresco Share chart

Alfresco is now deployed as a separate chart and can be enabled/disabled. In
order to do so simply use the value bellow:

```yaml
share:
 enabled: false
```

### Chart modularization: Alfresco Transform Service

`alfresco-content-service` now offers the ability to fully disable Alfresco
transformation service. It became possible as we have created a dedicated chart:
[alfresco-transform-service](https://github.com/Alfresco/alfresco-helm-charts/tree/main/charts/alfresco-transform-service)
This chart is enabled by default in `alfresco-content-service` but can be
disabled by setting `alfresco-transform-service.enabled` to `false`.
This change also incurs a modification of the `values.yaml` structure.
Previously, all transformer components used to be root objects in the YAML
values definition, and `transformmisc` was the only one that used to be
"toggle-able". Now all components' values should be placed under the root
`alfresco-transform-service` node, and each component can be enabled/disable
individually. So for example:

```yaml
transformmisc:
  enabled: true
  ...
```

Must be turned into:

```yaml
alfresco-transform-service:
  transformmisc:
    enabled: true
    ...
```

and should you want to disable jodconverter transformers you can do so by using:

```yaml
alfresco-transform-service:
  libreoffice:
    enabled: true
    ...
```

> Note: the values file contains an Anchor/Aliases to ensure and advertise a
> way to have some "backward compatibility" with previous values. That
mechanism do not propagate beyond the YAML file where it is defined so we
strongly recommend updating your `values.yaml` to reflect the changes described
above.

## 6.0.0

### Charts modularization

`alfresco-content-services` chart has always been the mandatory entrypoint to
deploy Alfresco platform and components. In order to provide more flexibility
we've started an effort of splitting Alfresco components into individual charts
that can be used independently.

That effort is work in progress and we've started by turning the previously
embedded subcharts into individual charts hosted in a new repository:
[alfresco-helm-charts](https://github.com/Alfresco/alfresco-helm-charts)

The associated registry is `https://alfresco.github.io/alfresco-helm-charts/`

These change comes with some deep modifications of the values structure:

#### Resources limits

We have introduced `resources.request` & `resources.limits` for each Alfresco
component deployment. The purpose is of course to avoid a single component
eating up all of the worker node's resource. Though, the default we provide
might not suit your workload and you MUST review them and align them in you
values in order to make sure your environment runs with appropriate amount of
resource.

Customizing resource allocation follow the generic kubernetes syntax under
each component's YAML node. For example for the ACS repo:

```yaml
repository:
    resources:
      requests:
        cpu: "0.5"
        memory: "1000Mi"
      limits:
        cpu: "1"
        memory: "1000Mi"
```

> You should focus on the limits to allow for more resource to be allocated to
> the pods while the requests are mostly present to avoid scheduling the node on
> too small worker nodes or requesting too much resources than needed.

#### Resources naming

The following charts benefited from a shift in the way resources are names.
We've tried to stick more closely to the Helm provided templates. That impacts
the charts in different ways and we advise you review changes for each chart or
deploy the new chart somewhere for tests and compare the resource names  if you
anticipate this change may be a problem for you and need to know about the new
names.

The list of charts which had some naming template modifications:

* [activemq](https://github.com/Alfresco/alfresco-helm-charts/tree/main/charts/activemq)
* [alfresco-search-enterprise](https://github.com/Alfresco/alfresco-helm-charts/tree/main/charts/alfresco-search-enterprise)
* [alfresco-search-service](https://github.com/Alfresco/alfresco-helm-charts/tree/main/charts/alfresco-search-service)
* [alfresco-sync-service](https://github.com/Alfresco/alfresco-helm-charts/tree/main/charts/alfresco-sync-service)

#### YAML nodes name remapping

We have changed part of the YAML structure of the `values.yaml` file.
Some changes should be transparent some other require to align you own values.

##### Transparent remapping (handled with a chart alias)

`alfresco-elasticsearch-connector` => `alfresco-search-enterprise`
`alfresco-search` => `alfresco-search-service`

##### Breaking remapping

`alfresco-admin-app` => `alfresco-control-center`
`alfresco-sync-service.syncservice` => `alfresco-sync-service`

## 5.4.0-M3

### Search Enterprise chart rename

The previous `alfresco-elasticsearch-connector` subchart has been renamed to
`alfresco-search-enterprise` to better reflect the product name during the
migration to the new
[alfresco-helm-charts](https://github.com/Alfresco/alfresco-helm-charts)
repository.

Accordingly to this chart rename, also the related values has been moved from
`.Values.alfresco-elasticsearch-connector` to
`.Values.alfresco-search-enterprise`.

The elasticsearch dependency (from elastic.co) has been moved from the main
chart to the new alfresco-search-enterprise, thus the Values has been moved
from `.Values.elasticsearch` to
`.Values.alfresco-search-enterprise.elasticsearch`

## 5.4.0-M2

### CPU resources

A default CPU resources requests and limits has been introduced to make sure
that Kubernetes scheduler has some more hints on how properly place pods on the
available nodes in a cluster.

That could be a breaking change for helm installations on cluster that has
**less than 10 cpu**.

You can fine tune CPU resources for each pod by updating the `resources` section
that is available for each component in their respective **values** file,
according to the standard [kubernetes resources
management](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#resource-units-in-kubernetes).

For example, in the [alfresco-content-services values
file](../../helm/alfresco-content-services/values.yaml) you can find:

```yaml
repository:
  replicaCount: 2
  resources:
    requests:
      cpu: "1"
      memory: "1500Mi"
    limits:
      cpu: "4"
      memory: "3000Mi"
```

That means that each `repository` pod will have a reservation of 1 full cpu core
and enables bursting up to 4 cpu cores. You can also reduce the number of
replicas for the components that allows it.

## 5.4.0-M1

### Persistence

Previous versions of the chart did not use that per-component approach to storage.
Instead, the default behavior was to create a PVC and rely by default on it for
any kind of data to persist). That approach has proven to cause problems and
that's why we're moving away from it.
However if you have already deployed using this approach and want to keep it
(which we don't recommend), you can do so by using the static provisioning approach
and set the `existingClaim` to the previously created PVC `alfresco-volume-claim`:

```yaml
postgresql:
  persistence:
    existingClaim: alfresco-volume-claim
```

Another option is to create a new volume and copy data to it from the old
volume bound to the old `alfresco-volume-claim`.
Details of this process depends on the type of storage and provisioner that
was used during deployment.

If you choose the second - and preferred - method, you'll then need to use
[static provisioning method](storage.md#configuring-static-provisioning) to
create a new volume and then instruct helm to search for a specific volume by
claim name or `storageClass`. Using `storageClass` requires creating a new PVC
too, which should reference the PV name to make sure a new volume is not
dynamically created.
Also,  applying `labels` to the PV and corresponding `selector` to the PVC
helps ensure the `storageClass` will only pick the intended volume.

## 5.3.0

### PostgreSQL persistence

Version 5.3.0 changes the way the default persistence is set up for the
PostgreSQL database. If you did not customize the database persistance (which
was not recommended for serious workloads). Please take a look at [this](./storage.md)
before trying to upgrade.

## 5.2.0

### Solr tracking shared secret

As of chart version 5.2.0 (ACS 7.2.0) it is now required to set a shared secret
for solr and repo to authenticate to each other.

```yaml
global:
  tracking:
    auth: secret
    sharedsecret: 50m3S3cretTh4t!s5tr0n6
```

If you are deploying ACS version pre 7.2.0 with charts version 5.2.0+, make
sure to set the value below to your `values.yml` file:

```yaml
global:
  tracking:
    auth: none
```

If you try to install ACS 7.2.0 and following versions, the configuration below
is **not supported** anymore and you are **required to set a shared secret**.

> :information_source: Due to protocol and ingress restrictions FTP is not
> exposed via the Helm chart.

## 5.0.0

### versioning

Version 5.0.0 and later of the ACS Helm chart has been updated to be version
agnostic, meaning the same chart can now be used to deploy different versions
of ACS.

By default the latest version of the chart will always deploy the latest
development version of ACS. A set of values files are also provided that can be
used to deploy a specific major.minor version.

> As the Helm chart no longer deploys a specific version of ACS the
`appVersion` property within the chart is longer be specified.
