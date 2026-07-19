- Need to create namespaces, can't apply them
- Need to add system:authenticated:oauth to userGroups
- tenant-a shows how to set defaults in a base kustomization
  - if we don't do this, we could put the defaults in the ansible automatin, but they would have to be hard coded in each overlay
  - annoying if we have to update the defaults, need to script with yq or something to update
- can't allow list labels/annotations for namespaces, need to deny list
  - [feature request](https://github.com/projectcapsule/capsule/issues/1501)
- Need to figure out installing with kustomize - currently just using helm install




- Initial install working - problem with security labels and annotations:

```bash
$ oc logs -n openshift-kube-controller-manager kube-controller-manager-control-plane-cluster-dn6bj-1 -c cluster-policy-controller | grep tenant-a
E0719 04:08:06.863114       1 base_controller.go:277] "Unhandled Error" err="\"namespace-security-allocation-controller\" controller failed to sync \"ns/tenant-a-test2\", err: admission webhook \"namespaces.validating.projectcapsule.dev\" denied the request: namespace annotations validation failed: openshift.io/sa.scc.supplemental-groups is forbidden for the current Tenant. Forbidden are matching the regex .*"
```
