# The Staging Environment 
The staging environment contains the Flask Application, Redis and MySQL within the staging K8s cluster's default namespace.<br>
MySQL is deployed without a persistent storage. Therefore, it will lose any information upon restart.<br> 
The secrets and config maps are also defined in this directory. 