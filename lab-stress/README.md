# stress-ng usage
```shell
k create -f stress-ng.yaml
# wait till the pod restarts
# Check the OOM
```

Add resources under container - name: stress-ng
```yaml
      resources:
        limits:
          cpu: '2'
          memory: "5Gi"
        requests:
          cpu: "1"
          memory: "3Gi"
```