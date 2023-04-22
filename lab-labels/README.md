# Labels and  Label Selectors

## Labels
Labels are key/value pairs that are attached to objects, such as pods. Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system. Labels can be used to organize and to select subsets of objects. Labels can be attached to objects at creation time and subsequently added and modified at any time. Each object can have a set of key/value labels defined. Each Key must be unique for a given object.

Labels allow for efficient queries and watches and are ideal for use in UIs and CLIs. Non-identifying information should be recorded using annotations

## Label Selectors
Unlike names and UIDs, labels do not provide uniqueness. In general, we expect many objects to carry the same label(s).
Via a label selector, the client/user can identify a set of objects. The label selector is the core grouping primitive in Kubernetes.

The API currently supports two types of selectors: **equality-based and set-based**.
**equality-based** is ```kubectl get pods -l environment=production,tier=frontend```  
**set-based** is ```kubectl get pods -l 'environment in (production),tier in (frontend)'```  

A label selector can be made of multiple requirements which are comma-separated. In the case of multiple requirements, all must be satisfied so the comma separator acts as a logical AND (&&) operator.

```shell
k create -f rs.yaml
k describe rs rs-one
k get pods
k get rs
k delete rs rs-one --cascade=orphan
k get rs
```
Create the ReplicaSet again. As long as we do not change the selector field, the new ReplicaSet should take
ownership. Pod software versions cannot be updated this way.
```shell
k create -f rs.yaml
```

We will now isolate a Pod from its ReplicaSet. Begin by editing the label of a Pod. We will change the system:
parameter to be IsolatedPod.
```shell
k edit po rs-one-xxxxx
```
See pod running 
```shell
k get po -L system
```
Delete replicaset
```shell
k delete rs rs-one
```
Delete remaining Pod using the label
```shell
k delete po -l system=IsolatedPod
```