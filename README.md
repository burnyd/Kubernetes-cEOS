# Kubernetes-cEOS
Running cEOS as a Kubernetes Pod. 

Please follow the readme within this doc on deploying cEOS.  First download the cEOS-lab.tar.xz file from the Arista software downloads page.

Afterwards on any running kubernetes cluster that has access to the ceosimage:4.20.5F image.

kubectl apply -f ceos.yaml 

This is not a CNI plugin just a way to run cEOS multiple times as a pod within Kubernetes.  To bridge and connect to the network or top of rack switch please look into the Intel NFV multus project within the 08-multus-cni.conf file for example. 
