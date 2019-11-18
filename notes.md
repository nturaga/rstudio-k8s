# Demo notes for May 10th

## What the hell is Kubernetes?? WHAT IS IT?

It basically helps you to "orchestrate" your containers locally or on
the cloud.

What does orchestrate mean? Synonyms: "Conduct" or "Conductor" ...sound familiar?

## Examples

We created two examples,

1. k8s-redis-bioc-example https://github.com/mtmorgan/k8s-redis-bioc-example

1. rstudio-k8s https://github.com/nturaga/rstudio-k8s

## How does docker come in to the picture?

Docker is a container engine, and hub.docker stores "images". Docker
images become containers when they are running. 

All the scripts needed to be run within the "container"-network or
pod-network need to be stored in the running container.

## Kubernetes or k8s

K8s on Google cloud (multi node - real deal)

or

Local `minikube` cluster (single node - testing)

## minikube vs gcloud demo

### Start a cluster

- minikube

		minikube start

- gcloud

NOTE: bioconductor-anvil is where we are billed

	gcloud config set project bioconductor-anvil

	gcloud container clusters create bioc-test --zone us-east4-b --num-nodes 4

	gcloud container clusters get-credentials bioc-test

### Create a deployment

Works exactly the same on both minikube and gcloud

	kubectl apply -f rstudio-k8s/deploy/

or if you take a look at the redis-param example,

	kubectl apply -f k8s-redis-bioc-example/k8s/

Create firewall to expose port

    gcloud compute firewall-rules create test-node-port --allow tcp:[NODE_PORT]


### Take a look at your deployment of services and pods

Using kubectl

	kubectl get all

or

	kubectl get services

	kubectl get pods

	kubectl get deployments

### Delete services

Using kubectl

	kubectl delete service rstudio-service

	kubectl delete pod rstudio-pod

	etc...

### Dashboard

Get a dashboard

	minikube dashboard

	kubectl proxy


### What is "helm"? 

https://github.com/galaxyproject/galaxy-kubernetes

