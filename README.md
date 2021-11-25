# Training Plan 

<img src="plan.png">

### Revision 

<img src="rev.png">

### k8s architecture 

<img src="apiserver.png">

### checking config view and connecting 

```
kubectl  get  no
NAME            STATUS   ROLES                  AGE   VERSION
control-plane   Ready    control-plane,master   24h   v1.22.4
node1           Ready    <none>                 24h   v1.22.4
node2           Ready    <none>                 24h   v1.22.4
 fire@ashutoshhs-MacBook-Air  ~  kubectl  config  view 
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://54.157.252.113:6443
  name: kubernetes
contexts:
- context:
    cluster: kubernetes
    user: kubernetes-admin
  name: kubernetes-admin@kubernetes
current-context: kubernetes-admin@kubernetes
kind: Config
preferences: {}
users:
- name: kubernetes-admin
  user:
    client-certificate-data: REDACTED
    client-key-data: REDACTED

```

### etcd 

<img src="etcd.png">

## to Get dashboard access 

### check port number

### check token 

```
 kubectl   get  secret  -n kubernetes-dashboard 
NAME                               TYPE                                  DATA   AGE
default-token-l5zkg                kubernetes.io/service-account-token   3      24h
kubernetes-dashboard-certs         Opaque                                0      24h
kubernetes-dashboard-csrf          Opaque                                1      24h
kubernetes-dashboard-key-holder    Opaque                                2      24h
kubernetes-dashboard-token-ndvgr   kubernetes.io/service-account-token   3      24h


=====

kubectl  describe  secret  kubernetes-dashboard-token-ndvgr    -n kubernetes-dashboard 
Name:         kubernetes-dashboard-token-ndvgr
Namespace:    kubernetes-dashboard
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: kubernetes-dashboard
              kubernetes.io/service-account.uid: b094c064-e3a8-47cc-be71-61c0ea12b072

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1099 bytes
namespace:  20 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6IlBiZUJmQkdmQUI4bHFpelpZZkxzTG9UaEZyNjJPX1AzbWNrTVpKSmlOcTQifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZ
```

### generate yaml / JSON output 

```
 7087  kubectl  run  ashupodx1  --image=nginx   --port 80 --dry-run=client -o yaml
 7088  kubectl  run  ashupodx1  --image=nginx   --port 80 --dry-run=client -o json 
```

### yaml file saved 

```
kubectl   run  ashupod3  --image=nginx --port 80 --dry-run=client -o yaml   >nginx.yaml

```

### replacing 

```
 kubectl  replace -f nginx.yaml  --force 
pod "ashupod3" deleted
pod/ashupod3 replaced

```

### namespace in k8s 

<img src="ns.png">

### checking namespace of pod 

<img src="ns1.png">

### list of namespaces 

```
kubectl   get  namespaces 
NAME                   STATUS   AGE
default                Active   25h
kube-node-lease        Active   25h
kube-public            Active   25h
kube-system            Active   25h
kubernetes-dashboard   Active   25h
 fire@ashutoshhs-MacBook-Air  ~  
 fire@ashutoshhs-MacBook-Air  ~  
 fire@ashutoshhs-MacBook-Air  ~  
 fire@ashutoshhs-MacBook-Air  ~  
 fire@ashutoshhs-MacBook-Air  ~  kubectl   get  ns         
NAME                   STATUS   AGE
default                Active   25h
kube-node-lease        Active   25h
kube-public            Active   25h
kube-system            Active   25h
kubernetes-dashboard   Active   25h

```

### checking pods with different namespace 

```
kubectl  get  po 
No resources found in default namespace.
 fire@ashutoshhs-MacBook-Air  ~  kubectl  get  po   -n  kube-public
No resources found in kube-public namespace.
 fire@ashutoshhs-MacBook-Air  ~  
 fire@ashutoshhs-MacBook-Air  ~  
 fire@ashutoshhs-MacBook-Air  ~  kubectl  get  po   -n  kubernetes-dashboard
NAME                                        READY   STATUS    RESTARTS      AGE
dashboard-metrics-scraper-c45b7869d-hnc8p   1/1     Running   2 (17h ago)   25h
kubernetes-dashboard-576cb95f94-xv78x       1/1     Running   2 (17h ago)   25h

```

### kube-system contains k8s internal components 

```
kubectl  get  po   -n  kube-system
NAME                                       READY   STATUS    RESTARTS      AGE
calico-kube-controllers-56b8f699d9-crgwn   1/1     Running   2 (17h ago)   25h
calico-node-54wxn                          1/1     Running   2 (17h ago)   25h
calico-node-7x46l                          1/1     Running   2 (17h ago)   25h
calico-node-9dnts                          1/1     Running   2 (17h ago)   25h
coredns-78fcd69978-7p8gh                   1/1     Running   2 (17h ago)   25h
coredns-78fcd69978-88lfh                   1/1     Running   2 (17h ago)   25h
etcd-control-plane                         1/1     Running   2 (17h ago)   25h
kube-apiserver-control-plane               1/1     Running   2 (17h ago)   25h
kube-controller-manager-control-plane      1/1     Running   2 (17h ago)   25h
kube-proxy-czq4d                           1/1     Running   2 (17h ago)   25h
kube-proxy-nqrlk                           1/1     Running   2 (17h ago)   25h
kube-proxy-vzztr                           1/1     Running   2 (17h ago)   25h
kube-scheduler-control-plane               1/1     Running   2 (17h ago)   25h
metrics-server-6fb5c69669-ngz66            1/1     Running   2 (17h ago)   25h

```

###  creating namespace 

```
kubectl   create  namespace   ashu-space  
namespace/ashu-space created
 fire@ashutoshhs-MacBook-Air  ~  kubectl  get  ns
NAME                   STATUS   AGE
ashu-space             Active   4s
default                Active   25h
kube-node-lease        Active   25h
kube-public            Active   25h
kube-system            Active   25h
kubernetes-dashboard   Active   25h


```

### setting default namespace 

```
kubectl  config  set-context  --current --namespace=ashu-space 
Context "kubernetes-admin@kubernetes" modified.
 fire@ashutoshhs-MacBook-Air  ~  kubectl  get  pods
No resources found in ashu-space namespace.

```

### checking default namespace 

```
kubectl  config  get-contexts 
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   ashu-space

```

### deploy pod in different namespace 

```
kubectl apply -f  ashupod1.yaml   -n  default 
pod/ashupod-1 created

```

### YAML with custom changes 

```
apiVersion: v1
kind: Pod
metadata:
  namespace: default # namespace information 
  creationTimestamp: null
  labels:
    run: ashupod3
  name: ashupod3 # name of pod 
spec:
  nodeName: node1 # static scheduling 
  containers:
  - image: nginx # docker image 
    name: ashupod3 # name of container 
    ports: # container app port number 
    - containerPort: 80
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}


```




