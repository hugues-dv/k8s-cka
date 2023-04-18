# k8s-cka
Training course for the cka certification

## First step
Go to kubespray directory and apply the README.md commands

## Kubernetes primitives
![primitives](screenshot/kubernetes_primitives.png)

## First commands
```
alias k='kubectl'  # alias
alias ll='ls -alrt'
source <( kubectl completion bash | sed s/kubectl/k/g )
k get nodes   # Check
k api-resources # list of kubernetes resources
```

## Deployment
![deployment](screenshot/deployment_relationship.png)


```shell
k create deployment app-cache --image=memcached:1.6.8 --replicas=4
k get po 
k get rs
k get deploy
k describe deploy # -> tab to find the object name 
```