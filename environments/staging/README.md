# The Staging Environment 
The staging environment contains the Flask Application, Redis and MySQL within the staging K8s cluster's default namespace.<br>
MySQL is deployed without a persistent storage. Therefore, it will lose any information upon restart.<br> 
The secrets and config maps are also defined in this directory. 

### Create a GKE cluster
Create a cluster - type: autopilot<br>
Change the cluster name, project and GKE zone in the [GitHub actions ci file](https://github.com/linux-training-group-1/asset-registry/blob/0bcd566e24d0c99a90e3aaba1026da0cd4a616c0/.github/workflows/ci.yml#L8) 
### Add the regcred secret for docker config file
The secret can be found here<br>
https://docs.google.com/document/d/1wPSJVYKU5EWj_Lu7uTDaZhxoQJK2BvIB11MB7hpQfmQ/edit#<br>
### Spinup a cloud shell
Copy the secret to a file<br>
![Screenshot from 2021-12-12 10-54-05](https://user-images.githubusercontent.com/32504465/145701482-95169c2c-3555-490b-bb0e-19ea83ef2f25.png)<br>
### use kubectl apply
`kubectl apply -f <file-name.yaml>`
### Deploy automatically
Trigger the CI pipeline<br>
You can push a commit or 're-run all jobs' button after selecting an action on the [Actions page](https://github.com/linux-training-group-1/asset-registry/actions)
---
## How to deploy manually
### Spinup a cloud shell after creating a cluster
### Download kustomize
This command will download the kustomize executable to the current directory
```
curl -s "https://raw.githubusercontent.com/kubernetes-sigs/kustomize/master/hack/install_kustomize.sh"  | bash
```
### Deploy with kubectl apply
```
kustomize build | kubectl apply -f -
```

