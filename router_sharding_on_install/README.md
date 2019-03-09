These settings configure router sharding by for two different domain on install.

An easy way to test this is to directly call ```ansible-playbook -i inventory /path/to/openshift-ansible/playbooks/openshift-hosted/deploy_router.yml```

and it will redeploy your routers.


To create your new route:

```
oc get svc
oc create route reencrypt mynewroute --hostname=myapp.domain-a.example.com --service=myservice
oc label route mynewroute router=domain-a
```
an `oc describe route mynewroute` should show that the domain-a router has picked up the route.

You can use plain oc expose commands if the router is configured to the cluster default subdomain, but that isn't recommended for consistency. 

This can cause some issues with certain operators, for example: The monitoring operator verifies the routes for grafana/prometheus resolve, and will remmain in a waiting state until those routes get manually labeled on install.

# TODO: Example route templates with the labels included.
