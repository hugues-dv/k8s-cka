# lab replicaset 
```shell
alias k = 'kubectl'
source <( kubectl completion bash | sed s/kubectl/k/g)
```
A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.

As soon as your cluster is set up you can check it but running the following commands.

```shell
k get node   # get list of nodes
k describe node  <node_name> # detail of nodes
k get nodes  # usage of plurals names
k get node -o wide # more info
```
The master won’t allow non-internal pods by default for security reasons.    
Allow the master server to run non-infrastructure pods.
The master node begins tainted for security and performance reasons.    
We will allow usage of the node in the training environment, but this step maybe skipped in a production environment.

```shell
k describe node | grep -i taint  # get taint
k taint nodes --all node-role.kubernetes.io/control-plane-  # remove taint
# check describe node | grep -i taint k 
k describe node | grep -i taint  # check if a taint is present
```

## ReplicaSet 
```shell
k create -f rs.yaml
```



