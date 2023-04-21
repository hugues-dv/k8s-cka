see all scripts
```shell
# Go on the master 
# BEWARE:  change the server ip address beforehand
k create -f pv.yaml   # create a persistentvolume
k get pv     # check persistentVolume
k get pvc    # check persistentVolumeClaim 
k create -f pvc.yaml   # create a persistentvolume
k get pvc   # Check 
k create -f nfs-pod.yaml  # install a pod connected to the pvc
k get pods    # Check 
k describe pod nginx-xxxxx  # verify  
```
## Resource Quota
```shell
k delete deployments.apps nginx-nfs 
k delete pvc pvc-one 
k delete pv pvvol-1 
k create namespace small
k describe ns small 
k  create -f pv.yaml  
k -n small create -f pvc.yaml 

k -n small create -f storage-quota.yaml 
k describe ns small
k -n small create -f nfs-rsquota.yaml 
k get deployments.apps -n small
k -n small describe deployments.apps nginx-nfs 
k -n small get pod
k -n small describe pod nginx-xxxx
k describe ns small

sudo dd if=/dev/zero of=/opt/sfw/bigfile bs=1M count=300
k describe ns small
du -h /opt
k -n small get deployments.apps 
k -n small delete deployments.apps nginx
k describe ns small
k -n small get pvc
k -n small delete pvc pvc-one 
k -n small get pv 
# see the status set to released
k delete pv pvvol-1 
k create -f pv.yaml 
kubectl patch pv pvvol-1 -p '{"spec":{"persistentVolumeReclaimPolicy":"Delete"}}'
# see the reclaim policy is set to Delete
k describe ns small
k -n small create -f pvc.yaml
k describe ns small
k -n small delete resourcequotas storagequota
k describe ns small
k -n small  create -f nfs-pod.yaml
```