# Governance as Code Demo

### Set up the Control plane
1. Create namespace for the control plane
```
oc new-project istio-system
```

2. Create OSSM control plane
```
oc apply -n istio-system -f controlplane.yaml
```

### Set up the bookinfo application
1. Create a new namespace to run the bookinfo application
```
oc new-project bookinfo
```

2. Create ServiceMeshMemberRoll resource to add bookinfo namespace to the service mesh
```
oc create -n istio-system -f servicemeshmemberroll-default.yaml
```

3. Verify that the ServiceMeshMemberRoll was created successfully
```
oc get smmr -n istio-system
```

You should see output similar to the following:

```
NAME      READY   STATUS       AGE
default   1/1     Configured   3m22s
```

4. From the CLI, deploy the Bookinfo application in the `bookinfo` project by applying the bookinfo.yaml file
```
oc apply -n bookinfo -f bookinfo/bookinfo.yaml
```

You should see output similar to the following:

```
service/details created
serviceaccount/bookinfo-details created
deployment.apps/details-v1 created
service/ratings created
serviceaccount/bookinfo-ratings created
deployment.apps/ratings-v1 created
service/reviews created
serviceaccount/bookinfo-reviews created
deployment.apps/reviews-v1 created
deployment.apps/reviews-v2 created
deployment.apps/reviews-v3 created
service/productpage created
serviceaccount/bookinfo-productpage created
deployment.apps/productpage-v1 created
```

5. Create the ingress gateway by applying the bookinfo-gateway.yaml file 
```
oc apply -n bookinfo -f bookinfo/bookinfo-gateway.yaml
```

You should see output similar to the following:
```
gateway.networking.istio.io/bookinfo-gateway created
virtualservice.networking.istio.io/bookinfo created
```

Set the value for the GATEWAY_URL parameter:
