# Creating a `Fragment` resource

### 1. Update git repo URL 
Update `spec.git.url` and `spec.git.ref.branch`

`fragments/tap-harel-workload-fragment.yaml`:
```yaml
apiVersion: accelerator.apps.tanzu.vmware.com/v1alpha1
kind: Fragment
metadata:
  name: tap-harel-workload
  namespace: accelerator-system
spec:
  displayName: "Tanzu Application Platform Workload Harel Git Repository Fragment"
  git:
    ref:
      branch: main
    url: https://github.com/terasky-int/harel-java-web-app.git
    subPath: fragments/tap-workload
```

### 2. Apply 
```bash
kubectl apply -f fragments/tap-harel-workload-fragment.yaml
```