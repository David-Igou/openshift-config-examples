LDAP is extremely frustrating to troubleshoot with openshift-ansible because the portion if the installation where it is configured is pretty long and you are subject to a lot of error between the ldap server, ldaps if used, and problems with openshift-ansible

This example has OUs with spaces, currently there is a bug where newlines get inserted by the openshift-ansibles yml parser at the first space in the `url` field. To avoid this, use %20 in place of spaces.


# Quickly troubleshooting LDAP AUTHENTICATION

To make this less painful:

```
ssh master01
# Point the oc client to https://localhost:8443
oc login https://localhost:8443
# Enter username/password, get authentication failed.

# Mess with settings
vi /etc/origin/master/master-config.yaml

#Restart services
/usr/local/bin/master-restart {api,controllers}
```

keep trying until you get the query right, once it's working shove it in your install files. Make sure to test with the installer (openshift-master install) to make sure the yml parser doesn't do anything weird when generating master-config

# Testing and automating LDAP Groupsync

```
oc adm groups sync --sync-config=path/to/sync.yml
# make sure query works, verify group
oc adm groups sync --sync-config=path/to/sync.yml --confirm
oc adm policy add-cluster-role-to-group cluster-admin my-group
```

