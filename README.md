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
k get no -o wide
k describe no master
```

## Deployment
The deployment is the central kubernetes primitive used for managing your application based on microservices.  


![deployment](screenshot/deployment_relationship.png)

### deployment with 3 replicas 
```shell
k create deploy -h | less
k create deployment nginx --image=nginx:1.24 --replicas=3
k get events
k get po 
k get rs
k get deploy
k get deploy,po,rs
k describe deploy # -> tab to find the object name 
k describe rs
k describe po
```
### Get yaml code source deployment 
```shell
k  get deploy nginx -o yaml >first.yaml
# copy first.yaml file and analyse
# delete lines displayed in gray color
# replace the status block of lines by status: {}
k delete deploy nginx
# k delete -f first.yaml
k create -f first.yaml
```
### Replica 
```shell
k delete po nginx-xxx 
```

### Service
The newly deployed nginx container is a light weight web server. We will need to create a service to view the default
welcome page. Begin by looking at the help output. Note that there are several examples given, about halfway through
the output.
```shell
k expose -h
```
Now try to gain access to the web server. As we have not declared a port to use you will receive an error.
```
kubectl expose deployment/nginx
```
To change an existing configuration in a cluster can be done with subcommands apply, edit or patch for non-disruptive
updates. The apply command does a three-way diff of previous, current, and supplied input to determine modifications
to make. Fields not mentioned are unaffected. The edit function performs a get, opens an editor, then an apply. You
can update API objects in place with JSON patch and merge patch or strategic merge patch functionality.
If the configuration has resource fields which cannot be updated once initialized then a disruptive update could be done
using the replace --force option. This deletes first then re-creates a resource.
```yaml
spec:
 containers:
 - image: nginx
   imagePullPolicy: Always
   name: nginx
   ports: # Add these
   - containerPort: 80 # three
     protocol: TCP # lines
   resources: {}
```
```shell
kubectl replace -f first.yaml
kubectl get deploy,pod
kubectl expose deployment/nginx
kubectl get svc nginx
kubectl get ep nginx
kubectl describe pod nginx-xxxx | grep Node:
k get pod -o wide
kubectl scale deployment nginx --replicas=3
# arreter tous les pods
kubectl scale deployment nginx --replicas=0
kubectl get deployment nginx
k get ep nginx
kubectl exec nginx-xxxxxx -- printenv |grep KUBERNETES
kubectl delete svc nginx
kubectl expose deployment nginx --type=NodePort
kubectl get svc
k get svc -A
```









## Outlines
* go to lab-etcd
* go to lab-pod   
* go to lab-dashboard
* go to lab-stress  
* go to lab-resource-limit  
* go to lab-replicaset
* go to lab-labels
* go to lab-daemonset
* go to lab-nfs
* go to lab-deployment
* go to lab-configmap
* go to lab-autoscaler
* go to lab-rollingupdate
* go to lab-taint-tolerations
