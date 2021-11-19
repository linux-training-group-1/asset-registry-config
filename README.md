# Asset Registry Config
This repository contains the K8s config files need to deploy the asset registry aplication.<br>

[Asset registry repo](https://github.com/linux-training-group-1/asset-registry) continas the CI pipeline that will build and push the application docker images. Then the CI agent (GitHub Actions) will update this repository with the new k8s configs (Ex: new docker image versions).<br>
Argo CD(Deployed on K8s cluster) will monitor this repo and pull any changes to the K8s cluster.

<br>
# Install ArgoCD on k8s cluster <br>

```
kubectl create namespace argocd
```

```
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
Create argo project and deploy the artifacts<br>
```
kubectl apply -f argocd/
```
Login to argocd server
```
kubectl port-forward -n argocd svc/argocd-server 8080:80
```
Username: admin<br>
Password: 
```
kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
```
copy the password and base64 decode it<br>
```
echo gvyuefgbvfiv | base64 --decode
```