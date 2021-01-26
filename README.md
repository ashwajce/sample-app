# Jenkins server and Sample application

This repo consists of a `jenkinsfile` to build sample application along with that helm chars to deploy Jenkins server & sample application.

# Prerequisites 
You need to install below applications/configuration before spinning up EKS cluster
- Helm 3
- kubectl binary
- Valid kubeconfig
- Docker (to build docker image in local)

# How to Install Jenkins sever
Please follow below steps to install Jenkins sever

Step 1:
After downloading kubeconfig, try to list the pods to see if you are able to connect to k8s cluster

```sh
$ helm install --name jenkins ./jenkins --namespace jenkins
```

Step 2:
After installing jenkins server & login using that credentials

```sh 
printf $(kubectl get secret --namespace jenkins jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo
```

Step 3: 
Configure this github repo and use `Jenkinsfile` to create a pipeline

Step 4: 
Run the pipeline to build & push the docker image

Step 5:
You can apply `sample-app-helm` chart to deploy to `sample-app` to eks cluster
```sh
$ helm install --name sample-app ./sample-app-helm
```
