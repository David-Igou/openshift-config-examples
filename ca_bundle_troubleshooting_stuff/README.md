# CA bundle troubleshooting stuff

If you are trying to kick off builds and are running into x509 errors this might help you. It is possible that your Openshift cluster and registry does not have the CA installed for your orgs docker registry.


If you are attempting to start builds, and are met with `BuildConfigInstantiateFailed` Check your imagestream with `oc describe is imagestream-being-used` to check for an x509. To resolve this:

```
ansible-playbook -i my-openshift-inventory os-install-root-ca.yml
ansible -i my-openshift-inventory -m service -a "name=docker state=restarted" nodes
```

If you are having builds fail with an x509 appearing in your build logs and `docker-registry` pod. You will need to add the ca to the deploymentconfig of the pod.


```
# This assumes os-install-root-ca.yml has been ran
ansible-playbook -i my-openshift-inventory openshift-registry-install-root-ca.yml
```
