# The Production Environment 
The production environment contains the Flask Application, Redis within the production K8s cluster's default namespace, Mysql outside the K8s cluster.<br>
ArgoDC runs in argocd namespace and fluentd runs in fluentd namespace.<br>
Config map will be created/updated at each deployment. But secrets have to be created separately, 
after initialization of the cluster<br>