I always forget this command so I'm putting it here

```
/usr/bin/oc --config=/etc/origin/master/admin.kubeconfig -n default volume dc/docker-registry --add --overwrite -t persistentVolumeClaim --claim-name=registry-claim --name=registry-storage --claim-size "{{ openshift_hosted_registry_storage_volume_size }}
```


