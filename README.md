# Capstone
Cloud Capstone Project. 
There are 2 pipelines. Pipeline "Capstone Infra" is used to deploy the kubernetes cluster with worker nodes. 
Pipeline "Capstone" is used to build docker image, push it to docker hub, and deploy it to loadbalancer with rolling deployment.

The docker image is just a custom nginx Hello World html file.

deployment folder contains yaml files to setup the loadbalancer and rolling deployment.

infra folder contains the Jenkinsfile for "Capstone Infra".

Detail steps can be found in Description.docx folder.
