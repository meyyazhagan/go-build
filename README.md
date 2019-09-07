# CI/CD Pipeline for Go application

Hello! Here is the CI/CD pipeline for Go application 

## The Plan

The plan is to create CI/CD using Jenkins(Declarative pipeline) and deploy the Go application in local kubernetes cluster with Helm as a package manager.

Tools Picked:

* CI/CD - Jenkins

* Containerization - Docker

* Container Orchestration - Kubernetes

* Package Manager - Helm

## Summary

I have created a kubernetes cluster in my local environment using minikube and as a first step deployed jenkins and redis containers using Helm charts.

Here are the details for the same:

* Used the stable/jenkins charts from here(https://github.com/helm/charts/tree/master/stable/jenkins) with the values from ./app/jenkins-values.yaml

* Used the stable/redis charts from here(https://github.com/helm/charts/tree/master/stable/redis) with the app version of 5.0.5

We primarily used Jenkins Kubernetes Plugin(https://github.com/jenkinsci/kubernetes-plugin) to run dynamic agents in a Kubernetes/Docker environment. Once the build is triggered it dynamically creates the agents(In our case jnlp, docker and helm containers in K8 Pod)and do the docker and helming stuffs and throw the agents away. Jenkins declarative pipeline is available here: ./app/Jenkinsfile and it has all the information about dynamic agents and build and deployment stages for this pipeline. We also used pollSCM instead of webhook because this scenario is experimented in the local notebook environment. But as always webhooks must be prefferd over pollSCM.

Redis credentials are copied as kubernetes secrets and it is consumed by the Go application.

Please check the ./app/README.md to know more about Dockerization and Helming for the Go application.

## To sum up

This task is purely done for local environment. So we can do some enhancements like Kubernetes RBAC setup, push/pull the Helm Charts to/from private chart repository(chart museum) and etc.