# Update Openshift DNS

In the event you need your openshift nodes to point to new DNS servers, you will need to update `/etc/dnsmasq.d/origin-upstream-dns.conf` and restart dnsmasq.

This is because Openshift runs a local DNS server for pods to resolve from and you will need to update the upstream server.
