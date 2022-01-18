# Asset Registry Config

This repository contains the K8s config files need to deploy the [asset registry application](https://github.com/linux-training-group-1/asset-registry).<br>

Setup guide for the Staging environment: [staging](/environments/staging/README.md)<br>
Setup guide for the Production environment: [production](/environments/production/README.md)

Staging and Production environment are two serpetrate k8s namespaces. 

The production environment: <br>

![LT full deployment](https://user-images.githubusercontent.com/32504465/149806430-d612c1d2-2621-42dc-b7cf-f0ff1da972e8.png)


The flow:

![argopull](https://user-images.githubusercontent.com/32504465/149806199-e1574998-607c-416b-94be-81f92135f40a.png)
Please not that logging namespace which runs fluentd is not shown here.
