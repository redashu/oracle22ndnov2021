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


