# Openshift Prometheus Federation

There are times where an org adopting Openshift might already have an instance of Prometheus running. You can configure that installation to scrape Openshift's Prometheus and federate the metrics. You can apply filters to this, and gain some flexibility, such as having a short retention on your cluster but have them scraped to something longer term.


