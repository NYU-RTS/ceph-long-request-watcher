# Ceph long request watcher

This is an exporter for Prometheus. It reports Ceph requests from the Linux kernel that take a long time, allowing Prometheus to trigger an alert that something is wrong with the cluster.

It is suitable for both RBD and CephFS kernel mounts as it will report both stuck metadata requests (to mds) and stuck data requests (to OSDs).

The exposed metrics are two gauges:

- `longest_request_seconds`, duration of the longest OSD request currently in progress
- `longest_mds_request_seconds`, duration of the longest MDS request currently in progress

If either of those metrics rise to multiple seconds, something is wrong with your cluster or network.

## Debug endpoint

There is an additional HTTP endpoint at `/requests` that will show the full list of requests currently in progress. This can help you pinpoint which OSD or MDS is stalling.
