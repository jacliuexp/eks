### Find all the resource in namespace
```
kubectl -n jupyter get svc,deploy,ds,sts,cm,secret,netpol,role,rolebinding,pvc,serviceintentions
```
```
NAMES="$(kubectl api-resources \
                 --namespaced \
                 --verbs list \
                 -o name \
           | tr '\n' ,)"

# ${NAMES:0:-1} -- because of `tr` command added trailing comma
# --show-kind is optional
kubectl get "${NAMES:0:-1}" --show-kind
```
```
kgetall='kubectl get namespace,replicaset,secret,nodes,job,daemonset,statefulset,ingress,configmap,pv,pvc,service,deployment,pod --all-namespaces'
```

```
for resource in [$(kubectl api-resources -o name | tr "\n" " ")]
do 
  kubectl get $resource --all-namespaces -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}'
done
```
