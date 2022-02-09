# Governance as Code Demo

### Create namespace for the control plane
```
oc new-project istio-system
```

### Create OSSM control plan
```
oc apply -n istio-system -f controlplane.yaml
```

### Create a new namespace to run the bookinfo application
```
oc new-project bookinfo
```

### Create ServiceMeshMemberRoll resource to add bookinfo namespace to the service mesh
```
oc create -n istio-system -f servicemeshmemberroll-default.yaml
```

### Verify that the ServiceMeshMemberRoll was created successfully
```
oc get smmr -n istio-system
```

```
NAME      READY   STATUS       AGE
default   1/1     Configured   3m22s
```

### 
