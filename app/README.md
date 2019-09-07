# ERVCP

ERVCP is a first in it's class, one of a kind Enterprise-Ready Visitor Counting Platform. Every time someone visits your website, the counter goes up.

## Dependencies

This application is written in [Go](https://golang.org/). Supported version is `1.12`.

This application uses [Redis](https://redis.io/) to store the data. Supported version is `5.0`.

## Configuring

This application is configured via environment variables:

* `ERVCP_PORT` - port, on which web app will run; defaults to `8080`
* `ERVCP_DB_HOST` - Redis host
* `ERVCP_DB_PORT` - Redis port
* `ERVCP_DB_PW` - Redis password

## Docker, Kubernetes and Helm

* Docker - We used multi-stage builds to keep the image size down. Hence the deployment will be faster and much more effective.

* Kubernetes - All the kubernetes yaml files are available under ./K8s/ directory. Under which we have used ConfigMaps to decouple configuration artifcats from image content to keep the application portable across environments, used secrets to store the database/repository credentials(AWS secret manager/Azure Key vault can be preferred to fetch the secret values rather than storing it in the repository), used Ingress resources to allow access to the application from the external world to the services inside K8 cluster(Ingress doesn't require external load balancer in AWS/Azure for every resource which could eventually save $$$$$) and deployment has all the details about the containers, environment variables, replicas, health probes for the application. Since we have multiple kubernetes objects to handle it will become complex down the line. So please read further.

* Helm - Package Manager for Kubernetes. Helm chart is available under ./gochart directory. Helm charts are developed in such a way that all the values will come from ./gochart/values.yaml as the values might be unique for each environments. Hence the ./gochart/templates directory will be much more cleaner with kubernetes yaml files to fetch the values dynamically. With helm we can easily rollback the release if required.

***Happy Dockerize and Helming in a Kubernetes Cluster!!***