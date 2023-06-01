# Install `harel-java-web-app` Tanzu Application Platform Accelerator

<!-- TOC -->
  * [Steps](#steps)
    * [1. Install `tap-harel-workload` `Fragment` resource](#1-install-tap-harel-workload-fragment-resource)
        * [1. Update git repo URL and branch](#1-update-git-repo-url-and-branch)
        * [2. Apply](#2-apply)
        * [3. Verify fragment](#3-verify-fragment)
    * [2. Install `harel-java-web-app` `Accelerator` resource](#2-install-harel-java-web-app-accelerator-resource)
        * [1. Update git repo URL and branch](#1-update-git-repo-url-and-branch)
        * [2. Apply](#2-apply)
        * [3. Verify accelerator](#3-verify-accelerator)
        * [4. (Optional) Reconcile](#4--optional--reconcile)
<!-- TOC -->

## Steps
### 1. Install `tap-harel-workload` `Fragment` resource

##### 1. Update git repo URL and branch

- **Update**: `spec.git.url` and `spec.git.ref.branch` in `fragments/tap-harel-workload-fragment.yaml` file.

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

##### 2. Apply
```bash
kubectl apply -f fragments/tap-harel-workload-fragment.yaml
```
**output**:
```bash
fragment.accelerator.apps.tanzu.vmware.com/tap-harel-workload created
```

##### 3. Verify fragment
```bash
kubectl get fragment tap-harel-workload -n accelerator-system 
```
**output**:
```bash
NAME                 READY   REASON   AGE
tap-harel-workload   True    Ready    57s
```

### 2. Install `harel-java-web-app` `Accelerator` resource

##### 1. Update git repo URL and branch
- **Update**: `spec.git.url` and `spec.git.ref.branch` in `docs/harel.yaml` file.

`docs/harel.yaml`:
```yaml
apiVersion: accelerator.apps.tanzu.vmware.com/v1alpha1
kind: Accelerator
metadata:
  name: harel-java-web-app
  namespace: accelerator-system
spec:
  git:
    url: https://github.com/terasky-int/harel-java-web-app.git
    ref:
      branch: main
```

##### 2. Apply
```bash
kubectl apply -f docs/harel.yaml
```
**output**:
```bash
accelerator.apps.tanzu.vmware.com/harel-java-web-app created
```

##### 3. Verify accelerator
```bash
kubectl get accelerator harel-java-web-app -n accelerator-system
```
**output**:
```bash
NAME                 READY   REASON   AGE
harel-java-web-app   True    Ready    19d
```

##### 4. (Optional) Reconcile
In case of any changes made to this accelerator, you can trigger a manual reconciliation, instead of waiting for TAP to pick up the changes pushed to git.
```bash
tanzu accelerator update <accelerator-name> --reconcile

# for example
tanzu accelerator update harel-java-web-app --reconcile
```