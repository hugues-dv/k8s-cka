# Resource limit


## use of namespace 
In Kubernetes, namespaces provides a mechanism for isolating groups of resources within a single cluster. Names of resources need to be unique within a namespace, but not across namespaces. Namespace-based scoping is applicable only for namespaced objects (e.g. Deployments, Services, etc) and not for cluster-wide objects (e.g. StorageClass, Nodes, PersistentVolumes, etc).

Namespaces provide a scope for names. Names of resources need to be unique within a namespace, but not across namespaces. Namespaces cannot be nested inside one another and each Kubernetes resource can only be in one namespace.

Namespaces are a way to divide cluster resources between multiple users (via resource quota).

```shell
k create namespace low-usage-limit
k get namespace
k get ns
```

## Limit range
```shell
k create -n low-usage-limit -f low-resource-range.yaml
k get LimitRange
k get LimitRange -A
```

## New stress-ng pod
```shell
k -n low-usage-limit create -f ../lab-stress/stress-ng.yaml
```
