# The Staging Environment 
The staging environment contains the Flask Application, Redis and MySQL within the staging K8s cluster's default namespace.<br>
MySQL is deployed without a persistent storage. Therefore, it will lose any information upon restart.<br> 
The secrets and config maps are also defined in this directory. 

### Create a GKE cluster
Create a cluster; name=cluster-1<br>
Change the cluster name, project and GKE zone in the [GitHub actions ci file](https://github.com/linux-training-group-1/asset-registry/blob/0bcd566e24d0c99a90e3aaba1026da0cd4a616c0/.github/workflows/ci.yml#L8) 
### Add the regcred secret for docker registry config file
This config contains the credentials for the private docker registry.<br>
This secret can be found here<br>
https://docs.google.com/document/d/1wPSJVYKU5EWj_Lu7uTDaZhxoQJK2BvIB11MB7hpQfmQ/edit#<br>
### Spinup a cloud shell
Copy the secret to a file<br>
![cloud-shell](https://user-images.githubusercontent.com/32504465/145701482-95169c2c-3555-490b-bb0e-19ea83ef2f25.png)<br>
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
### Clone the repo
```
git clone https://github.com/linux-training-group-1/asset-registry-config.git
```
### Deploy with kubectl apply
```
./kustomize build asset-registry-config/environments/staging | kubectl apply -f -
```
### Expose mysql service
```
kubectl port-forward svc/mysql-service  3306:3306 &
```
This command will run in the background
### Add the sql tables and data
```
wget https://raw.githubusercontent.com/linux-training-group-1/asset-registry/main/scripts/table.sql
wget https://raw.githubusercontent.com/linux-training-group-1/asset-registry/main/scripts/inserts.sql
mysql -h localhost -P 3306 --protocol=tcp -u root --password=password < table.sql
mysql -h localhost -P 3306 --protocol=tcp -u root --password=password < inserts.sql
```
The table structure and the mysql user for the application is described in `table.sql`<br>
If the mysql password is incorrect, read the mysql-secret using `kubectl get secret mysql-secret -o yaml` and use `echo '<password>' | base64 --decode` to decode the root password<br>
Now the staging environment is ready to be used.<br>

Correctly configured staging environment should look like below:<br>

![workloads](https://user-images.githubusercontent.com/32504465/145707740-b6b78d87-3dd6-4f50-9865-0407b605bd81.png)
<br>
![services](https://user-images.githubusercontent.com/32504465/145707733-a5868d3e-276f-4ea4-9860-d2c3af6496e0.png)
<br>
![Screenshot from 2021-12-12 15-47-25](https://user-images.githubusercontent.com/32504465/145708554-c07c88fc-7f4b-4f48-b5b8-e05f13b38343.png)
<br>
Naviate to the Ingress's IP address to access the Asset application.

