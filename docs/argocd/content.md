## Installation and Configuration of ArgoCD

| Step | Details |
| ----------- | ----------- |
| 1 | Introduction |
| 2 | Via Kubernetes Manifest  |
| 3 | Via Helm |
| 4 | Via Autopilot |
| 5 | Expose ArgoCD UI |
| 6 | ArgoCD Authentication |
| 7 | ArgoCD CLI |



### 1. Introduction 
---

### 2. Via Kubernetes Manifest
---

Installation of ArgoCD on the Azure Kubernetes Service (AKS) is required to get started. We have already installed the AKS cluster.

Create a namespace
```
kubectl create namespace argocd
namespace/argocd created
```

Run the Manifest Files

```
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

customresourcedefinition.apiextensions.k8s.io/applications.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/applicationsets.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/appprojects.argoproj.io created
serviceaccount/argocd-application-controller created
serviceaccount/argocd-applicationset-controller created
serviceaccount/argocd-dex-server created
serviceaccount/argocd-notifications-controller created
serviceaccount/argocd-redis created
serviceaccount/argocd-repo-server created
serviceaccount/argocd-server created
role.rbac.authorization.k8s.io/argocd-application-controller created
role.rbac.authorization.k8s.io/argocd-applicationset-controller created
role.rbac.authorization.k8s.io/argocd-dex-server created
role.rbac.authorization.k8s.io/argocd-notifications-controller created
role.rbac.authorization.k8s.io/argocd-server created
clusterrole.rbac.authorization.k8s.io/argocd-application-controller created
clusterrole.rbac.authorization.k8s.io/argocd-server created
rolebinding.rbac.authorization.k8s.io/argocd-application-controller created
rolebinding.rbac.authorization.k8s.io/argocd-applicationset-controller created
rolebinding.rbac.authorization.k8s.io/argocd-dex-server created
rolebinding.rbac.authorization.k8s.io/argocd-notifications-controller created
rolebinding.rbac.authorization.k8s.io/argocd-server created
clusterrolebinding.rbac.authorization.k8s.io/argocd-application-controller created
clusterrolebinding.rbac.authorization.k8s.io/argocd-server created
configmap/argocd-cm created
configmap/argocd-cmd-params-cm created
configmap/argocd-gpg-keys-cm created
configmap/argocd-notifications-cm created
configmap/argocd-rbac-cm created
configmap/argocd-ssh-known-hosts-cm created
configmap/argocd-tls-certs-cm created
secret/argocd-notifications-secret created
secret/argocd-secret created
service/argocd-applicationset-controller created
service/argocd-dex-server created
service/argocd-metrics created
service/argocd-notifications-controller-metrics created
service/argocd-redis created
service/argocd-repo-server created
service/argocd-server created
service/argocd-server-metrics created
deployment.apps/argocd-applicationset-controller created
deployment.apps/argocd-dex-server created
deployment.apps/argocd-notifications-controller created
deployment.apps/argocd-redis created
deployment.apps/argocd-repo-server created
deployment.apps/argocd-server created
statefulset.apps/argocd-application-controller created
networkpolicy.networking.k8s.io/argocd-application-controller-network-policy created
networkpolicy.networking.k8s.io/argocd-applicationset-controller-network-policy created
networkpolicy.networking.k8s.io/argocd-dex-server-network-policy created
networkpolicy.networking.k8s.io/argocd-notifications-controller-network-policy created
networkpolicy.networking.k8s.io/argocd-redis-network-policy created
networkpolicy.networking.k8s.io/argocd-repo-server-network-policy created
networkpolicy.networking.k8s.io/argocd-server-network-policy created

```

### 5. Expose ArgoCD UI
---
Then you can do a port forward and make ArgoCD available in localhost.

```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
![image](https://github.com/swarajitroy/gitops/assets/20844803/a19e4680-30a3-474f-88be-e7020ab9ca96)


Or you can make the service/argocd-server as a loadbalancer 

```
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

Or expose it over public load balancer

```
kubectl get svc -n argocd
NAME                                      TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
argocd-applicationset-controller          ClusterIP      10.0.193.96    <none>          7000/TCP,8080/TCP            7m32s
argocd-dex-server                         ClusterIP      10.0.174.162   <none>          5556/TCP,5557/TCP,5558/TCP   7m31s
argocd-metrics                            ClusterIP      10.0.99.42     <none>          8082/TCP                     7m30s
argocd-notifications-controller-metrics   ClusterIP      10.0.77.243    <none>          9001/TCP                     7m29s
argocd-redis                              ClusterIP      10.0.70.133    <none>          6379/TCP                     7m28s
argocd-repo-server                        ClusterIP      10.0.142.128   <none>          8081/TCP,8084/TCP            7m27s
argocd-server                             LoadBalancer   10.0.31.249    20.252.46.244   80:31754/TCP,443:32042/TCP   16s
argocd-server-metrics                     ClusterIP      10.0.123.34    <none>          8083/TCP                     7m25s

```
![image](https://github.com/swarajitroy/gitops/assets/20844803/0eae470f-9437-45e0-9724-bbf9dc38cd3d)

### 6. ArgoCD Authentication 
---

The user id is admin and password is maintained in a secret called argocd-initial-admin-secret

```
kubectl get secrets -n argocd
NAME                          TYPE     DATA   AGE
argocd-initial-admin-secret   Opaque   1      36m
argocd-notifications-secret   Opaque   0      37m
argocd-secret                 Opaque   5      37m
```
Get the password from the secret and do a base64 decode and you will be able to login to ArgoCD over UI.

![image](https://github.com/swarajitroy/gitops/assets/20844803/65243d4f-1849-4e63-8e7d-c7bf09b3ef6c)


 ### 7. ArgoCD CLI 
 ---
 Use this page for installation instruction 
 https://argo-cd.readthedocs.io/en/stable/cli_installation/ 

 I have used the following for my windows laptop

 ```
$url = "https://github.com/argoproj/argo-cd/releases/download/" + $version + "/argocd-windows-amd64.exe"
>> $output = "argocd.exe"
>> 
>> Invoke-WebRequest -Uri $url -OutFile $output
```

```
C:\swararoy\installers\argocd\argocd version                               
argocd: v2.8.4+c279299       
  BuildDate: 2023-09-13T19:43:37Z
  GitCommit: c27929928104dc37b937764baf65f38b78930e59
  GitTreeState: clean
  GoVersion: go1.20.7
  Compiler: gc
  Platform: windows/amd64
time="2023-10-05T09:55:15+05:30" level=fatal msg="Argo CD server address unspecified"

```

```
C:\swararoy\installers\argocd\argocd login 20.252.46.244
WARNING: server certificate had error: tls: failed to verify certificate: x509: certificate signed by unknown authority. Proceed insecurely (y/n)? y
Username: admin
Password:
'admin:login' logged in successfully
Context '20.252.46.244' updated

```

 

