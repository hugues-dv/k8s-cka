# Imperative et Declarative Commandees
## Imperative command for creating a pod
```shell
k run nginx --image=nginx  --port=8080
```

## Declarative command for creation pod using a YAML file
```shell
cd 
cd k8s-cka
cd lab-pod
kubectl get pod nginx -o yaml > pod-nginx.yaml
```
 
## Using init containers

Because init containers have separate images from app containers, they have some advantages for start-up related code:

    Init containers can contain utilities or custom code for setup that are not present in an app image. For example, there is no need to make an image FROM another image just to use a tool like sed, awk, python, or dig during setup.
    The application image builder and deployer roles can work independently without the need to jointly build a single app image.
    Init containers can run with a different view of the filesystem than app containers in the same Pod. Consequently, they can be given access to Secrets that app containers cannot access.
    Because init containers run to completion before any app containers start, init containers offer a mechanism to block or delay app container startup until a set of preconditions are met. Once preconditions are met, all of the app containers in a Pod can start in parallel.
    Init containers can securely run utilities or custom code that would otherwise make an app container image less secure. By keeping unnecessary tools separate you can limit the attack surface of your app container image.

```shell
k create -f nginx-initcontainer.yaml
```


## Check 
```shell
kubectl exec -it nginx -c nginx -- /bin/bash
```

## sidecar container
```shell
k create -f pod_with_sidecar.yaml

```
