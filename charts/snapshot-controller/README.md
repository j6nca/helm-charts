# snapshot-controller

Bundling a quick helm chart out of the manifests from [kubernetes-csi/external-snapshotter](https://github.com/kubernetes-csi/external-snapshotter)

## Updating

```
set APP_VERSION v8.2.0
# Grab CRDs
curl -fsSL https://raw.githubusercontent.com/kubernetes-csi/external-snapshotter/$APP_VERSION/client/config/crd/snapshot.storage.k8s.io_volumesnapshotclasses.yaml -o crds/snapshot.storage.k8s.io_volumesnapshotclasses.yaml
curl -fsSL https://raw.githubusercontent.com/kubernetes-csi/external-snapshotter/$APP_VERSION/client/config/crd/snapshot.storage.k8s.io_volumesnapshots.yaml -o crds/snapshot.storage.k8s.io_volumesnapshots.yaml
curl -fsSL https://raw.githubusercontent.com/kubernetes-csi/external-snapshotter/$APP_VERSION/client/config/crd/snapshot.storage.k8s.io_volumesnapshotcontents.yaml -o crds/snapshot.storage.k8s.io_volumesnapshotcontents.yaml
curl -fsSL https://raw.githubusercontent.com/kubernetes-csi/external-snapshotter/$APP_VERSION/client/config/crd/groupsnapshot.storage.k8s.io_volumegroupsnapshotclasses.yaml -o crds/groupsnapshot.storage.k8s.io_volumegroupsnapshotclasses.yaml
curl -fsSL https://raw.githubusercontent.com/kubernetes-csi/external-snapshotter/$APP_VERSION/client/config/crd/groupsnapshot.storage.k8s.io_volumegroupsnapshotcontents.yaml -o crds/groupsnapshot.storage.k8s.io_volumegroupsnapshotcontents.yaml
curl -fsSL https://raw.githubusercontent.com/kubernetes-csi/external-snapshotter/$APP_VERSION/client/config/crd/groupsnapshot.storage.k8s.io_volumegroupsnapshots.yaml -o crds/groupsnapshot.storage.k8s.io_volumegroupsnapshots.yaml

# Grab Resources
curl -fsSL https://raw.githubusercontent.com/kubernetes-csi/external-snapshotter/$APP_VERSION/deploy/kubernetes/snapshot-controller/setup-snapshot-controller.yaml -o templates/deployment.yaml
curl -fsSL https://raw.githubusercontent.com/kubernetes-csi/external-snapshotter/$APP_VERSION/deploy/kubernetes/snapshot-controller/rbac-snapshot-controller.yaml -o templates/rbac.yaml
```
