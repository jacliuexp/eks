##### Find all the resource in namespace
```
kubectl -n jupyter get svc,deploy,ds,sts,cm,secret,netpol,role,rolebinding,pvc,serviceintentions
```
```
k -n monitoring get svc,deploy,ds,sts,cm,secret,sa,pdb,netpol,role,rolebinding,pvc,serviceintentions --no-headers=true -o name | awk -F "/" '{print "kubectl -n monitoring get "  $1 " "  $2 " -o yaml | kubectl neat >"  $1"-"$2".yml"}'  > a.txt

# kubectl -n monitoring get service alertmanager-main -o yaml | kubectl neat >service-alertmanager-main.yml


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

##### Run Command/Args 
```
  containers:
  - name: my-container
    image: my-image:latest
    imagePullPolicy: Always
    ports:
    - containerPort: 80
    command: [ "/bin/bash", "-c" ]
    args:
     - 
        echo "check if my service is running and run commands";
        while true; do
            service my-service status > /dev/null || service my-service start;
            if condition; then
                    echo "run commands";
            else
                    echo "run another command";
            fi;
        done
        echo "command completed, proceed ....";
```
##### Get only resource names: like pod names
```
k -n monitoring get prometheusrule --no-headers -o custom-columns=":metadata.name"
k -n monitoring get secret alertmanager-main -o json  | jq -r 

$ cat a.sh
input="list.txt"
while read -r line
do
  echo "kubectl  -n monitoring get prometheusrule $line -o yaml >$line.yaml"
done < "$input"
```
##### Work over the {{ in helm
```
# escape brace curly
1.      proxy.token: "{{ .proxy.token }}"    
        {{ $openblock := "\x7B\x7B" }}
        {{ $closeblock := "\x7D\x7D" }}
        proxy.token: "{{ $openblock }}.mykey{{ $closeblock }}"
2.  {{ => {{ "{{" }}
    }} => {{ "}}" }}
    ex: {{ aaa }} =>  {{ "{{" }} aaa {{ "}}" }}
```
##### JQ key contains quote
```
 k -n monitoring get secret alertmanager-main -o json  | jq -r '.data."alertmanager.yaml"'
```
##### kubectl debug
https://kubernetes.io/docs/tasks/configure-pod-container/share-process-namespace/
```
k debug mypod --image=curlimages/curl -it  -- sh
k debug mypod -it --image=nginx --target=container1 -- bash
kubectl debug -it ephemeral-demo --image=busybox:1.28 --target=ephemeral-demo
```
##### node session
```
kubectl node-ssm start-session --target ip-10-10-10-10.ec2.internal
```
##### EKS upgrae
https://repost.aws/knowledge-center/eks-plan-upgrade-cluster
```
kubent  # check deprecated APIs
```

