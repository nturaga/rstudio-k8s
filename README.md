# Run Rstudio provided by rocker on kubernetes

This is a trial done on minikube cluster (single node cluster on my local machine)

## Running Rstudio in k8s

Steps:

Start minikube

	minikube start

Run the rstudio service

	kubectl run rstudio --image=rocker/rstudio --port=8787 --env="PASSWORD=bioc"

expose the deployment's nodeport so the host machine can see the
Rstudio instance being served on a browser

	kubectl expose deployment rstudio --target-port=8787 --name=rstudio-server --type=NodePort

Get minikube IP, this is where you'll find Rstudio

	minikube ip

Get the TCP port on the rstudio service

	kubectl get all


## Using the yaml files

Instead of running the above commands, use the yaml files

	kubectl create -f rstudio-service.yaml

	kubectle create -f rstudio-pod.yaml

Check if everything is running,

	kubectl get all

Delete services and pods as needed

	kubectl detele pod rstudio-pod

	kubectl delete service rstudio-service

## Mounting volumes on minikube

To mount a volume, you first need to mount a directory to the minikube
cluster, before it can be seen by the pod

	minikube mount ~/shared:/home/rstudio

Then, since the `rstudio-pod.yaml` file is set up to see that mount
path, you should be able to mount files/data as needed on that shared
volume.

NOTE: The above command to `minikube mount` has to be run before it
can be shared by the pod network

https://stackoverflow.com/questions/48534980/mount-local-directory-into-pod-in-minikube

https://github.com/kubernetes/minikube/blob/master/docs/host_folder_mount.md
