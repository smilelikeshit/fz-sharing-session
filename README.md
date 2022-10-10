

## Requirements ##
- 


### Create Cluster ###
```bash
imam@ThinkPad:~/learning-kind$ minikube start
😄  minikube v1.25.1 on Ubuntu 20.04
🎉  minikube 1.27.1 is available! Download it: https://github.com/kubernetes/minikube/releases/tag/v1.27.1
💡  To disable this notice, run: 'minikube config set WantUpdateNotification false'

✨  Automatically selected the docker driver
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
🔥  Creating docker container (CPUs=2, Memory=4900MB) ...
🐳  Preparing Kubernetes v1.23.1 on Docker 20.10.12 ...
    ▪ kubelet.housekeeping-interval=5m
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: default-storageclass, storage-provisioner
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default


imam@ThinkPad:~/learning-kind$ kubectl get pods
No resources found in default namespace.

imam@ThinkPad:~/learning-kind$ kubectl get nodes
NAME       STATUS   ROLES                  AGE   VERSION
minikube   Ready    control-plane,master   71s   v1.23.1

```


### Build App Golang ###
- copy source code from https://echo.labstack.com/cookbook/crud/
- create Dockerfile
- create docker-compose
- run docker-compose
```bash
WARNING: Image for service app was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Creating app_app_1 ... done
Attaching to app_app_1
app_1  | 
app_1  |    ____    __
app_1  |   / __/___/ /  ___
app_1  |  / _// __/ _ \/ _ \
app_1  | /___/\__/_//_/\___/ v4.9.0
app_1  | High performance, minimalist Go web framework
app_1  | https://echo.labstack.com
app_1  | ____________________________________O/_______
app_1  |                                     O\
app_1  | ⇨ http server started on [::]:1323

```
 - docker build -t fz-sharing-session:v1 .
 - docker tag fz-sharing-session:v1 insignficant/fz-sharing-session:v1 



### Create Kustomize ###
- create file deploment.yaml
- create file service.yaml
- create file kustomization.yaml

```bash
kubectl apply -k .
kubectl delete -k .
```

### Create HELM ###

```bash
 helm create app
 cp values.yaml values-production.yaml 
 cp values.yaml values-staging.yaml
 helm upgrade --install app-bdg ./ -n default --values values-staging.yaml
 helm upgrade --install app-production ./ -n default  --values-production.yaml

 imam@ThinkPad:~/project-fazpass/tmp/fz-sharing-session/tools/helm$ kp
NAME                                   READY   STATUS        RESTARTS         AGE   IP           NODE       NOMINATED NODE   READINESS GATES
app-6459dd6d6f-2cfhl                   1/1     Running       0                68m   172.17.0.3   minikube   <none>           <none>
app-bdg-5dfc757457-dhwjv               1/1     Running       0                51m   172.17.0.4   minikube   <none>           <none>
app-production-d55d5b8fc-qr2jn         1/1     Running       0                49m   172.17.0.5   minikube   <none>           <none>
```


### Install ArgoCD ##
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/core-install.yaml
kubectl port-forward svc/argocd-server -n argocd 8080:443
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
- access to localhost:8080
- create file application-kustomize.yaml
- create file application-helm.yaml

```bash
kubectl apply -f application-kustomize.yaml
kubectl apply -f application-helm.yaml
kubectl get app -n argocd
NAME        SYNC STATUS   HEALTH STATUS
helm        Synced        Healthy
kustomize   Synced        Healthy
```

###

