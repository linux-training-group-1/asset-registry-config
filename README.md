# Asset Registry Config
This repository contains the K8s config files need to deploy the asset registry aplication.<br>

[Asset registry repo](https://github.com/linux-training-group-1/asset-registry) continas the CI pipeline that will build and push the application docker images. Then the CI agent (GitHub Actions) will update this repository with the new k8s configs (Ex: new docker image versions).<br>
Argo CD(Deployed on K8s cluster) will monitor this repo and pull any changes to the K8s cluster.

