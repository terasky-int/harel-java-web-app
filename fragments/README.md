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
    subPath: fragments/tap-harel-workload
```

### 2. Apply 
```bash
kubectl apply -f fragments/tap-harel-workload-fragment.yaml
```
**output**:
```bash
fragment.accelerator.apps.tanzu.vmware.com/tap-harel-workload created
```

### 3. Verify
##### a. Verify fragment
```bash
kubectl get fragment tap-harel-workload -n accelerator-system 
```
**output**:
```bash
NAME                 READY   REASON   AGE
tap-harel-workload   True    Ready    57s
```

##### b. Verify accelerator
```bash
kubectl get accelerator harel-java-web-app -n accelerator-system
```
**output**:
```bash
NAME                 READY   REASON   AGE
harel-java-web-app   True    Ready    19d
```