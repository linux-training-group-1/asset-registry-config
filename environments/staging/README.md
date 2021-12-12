# The Staging Environment 
The staging environment contains the Flask Application, Redis and MySQL within the staging K8s cluster's default namespace.<br>
MySQL is deployed without a persistent storage. Therefore, it will lose any information upon restart.<br> 
The secrets and config maps are also defined in this directory. 

### Create a GKE autopilot cluster
Change the cluster name, project and GKE zone in the [GitHub actions ci file](https://github.com/linux-training-group-1/asset-registry/blob/0bcd566e24d0c99a90e3aaba1026da0cd4a616c0/.github/workflows/ci.yml#L8) 
### Add the regcred secret for docker config file
The secret can be found here

https://docs.google.com/document/d/1wPSJVYKU5EWj_Lu7uTDaZhxoQJK2BvIB11MB7hpQfmQ/edit#
#### Spinup a cloud shell
Copy the secret to a file
#### use kubectl apply
`kubectl apply -f <file-name.yaml>`