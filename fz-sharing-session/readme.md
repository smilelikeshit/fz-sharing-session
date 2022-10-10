

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