3 node processes:
1. Kubelet
2. Kube Proxy
3. Container runtime
Master Nodes

Master node controls all nodes

Client
Update or query

Master Node
Api Server (is the cluster healthy) (UI, API, CLI)
scheduler (check for cpu or memory resource and scale new pods or restart old pods)
Controller manager(detects cluster state change, if pods dies)
etcd(etcd is state manager)

Worker Node
docker
kubctl
pods

Example Cluster Set-up
2 Master nodes
3 worker nodes

Add new master/node server
1. get new bare server
2. install all the master/worker node processes
3. add it into cluster

minikube (used for testing in local machine)
where master and worker processes in same node

-> creates virtual box on your laptop
-> node runs in that virtual box

kubctl
kubernetes cli used to connect with api server for deployment

installation in local computer
1. brew install minikube
2. brew install hyperkit, brew install qemu
3. minikube start --driver=qemu
kubectl version  --output=json
minikube status
kubectl get nodes

basic kubectl commands
CRUD commands
create deployment - kubectl create deployment
edit deployment - kubectl edit deployment
delete deployment - kubectl deployment

status of different k8s components
kubectl get nodes|pod|services|replicaset|deployment

debugging pods
log to console - kubectl logs [pod name]
get interactive terminal - kubectl ecec -it [pod name] -- bin/bash

kubectl create deployment NAME --image=image [--dry-run] [options]
kubectl create deployment nginx-depl --image=nginx

deployment
- blueprint for creating pods
- most basic configuration for deployment(name and image to use)

- rest defaults

kubectl get replicaset
kubectl edit deployment nginx-depl

Layers of abstraction
deployment manages a replicaset
replicaset manages all replicaes of pods
pod is an abstraction of container


Debugging pods
kubectl create deployment mongo-depl --image=mongo
kubectl logs mongo-depl-79585f75cf-q2fqz
kubectl describe pod mongo-depl-79585f75cf-q2fqz

# To get inside mongodb container
kubectl exec -it mongo-depl-79585f75cf-q2fqz -- bin/bash
kubectl delete deployment mongo-depl
kubectl create deployment name image option1 option2
get pod -o wide
kubectl get deployment my-nginx -o yaml
kubectl get deployment my-nginx -o yaml > nginx-deployment-result.yaml
kubectl delete -f nginx-deployment-result.yaml 
kubectl get all

# To create deployment using config file
kubectl apply -f config-file.yaml

YAML configuration file in kubernetes
Overview
	- The three parts of configuration file
    - connecting deployments to service to pods
    - demo

configuration file

1. metadeta
2. specification

How to make external service
- type: "Loadbalancer"
..assigns service an external IP address and so accepts external requests

Namespace
	-> Organise resources in namespaces
	-> virtual cluster inside a cluster
	-> 4 namespaces per default

kubectl get namespaces
kubectl cluster-info
kubectl create namespace my-namespace
kubectl get namespace

Resource Sharing: Blue/Green Deployment
(versioning of production)


You can't access most resources from another namesapace
kubectl apply -f mysql-configmap.yaml --namespace=my-namespace
kubectl get configmap -n my-namespace

brew install kubectx

To check active namespace 
kubens

To change namespace
kubens my-namespace

External service vs ingress
Ingress yaml for domain name instead of ip and port

Pod <- my-app service <- my-app ingress <- ingress controller pod

Ingress controller
- evaluates all the rules
- manages redirections
- entrypoint to cluster
- many third party implementations
- k8s Nginx Ingress Controller

add ingress controller in minikube
minikube addons enable ingress
kubectl get pod -n kube-system

kubectl get ingress -n kubernetes-dashboard --watch
kubectl describe ingress dashboard-ingress -n kubernetes-dashboard
🔗 Links:
- Install Minikube (Mac, Linux and Windows): https://bit.ly/38bLcJy 
- Install Kubectl: https://bit.ly/32bSI2Z
- Gitlab: If you are using Mac, you can follow along the commands. I listed them all here: https://bit.ly/3oZzuHY

What is Helm?
1. package manager for kubernetes
2. To package yaml files
3. and distribute them in public and private repositories
Stateful Set
ConfigMap
K8s User with permissions
Secret
Services

helm search keyword
templating engine
Helm chart

types of orchestration tools
-> ECS
-> Docker swarm
-> kubernetes
-> mesos
-> nomad

eks commands

eksctl create cluster --name tp-cluster --region us-east-1 --fargate

pip install pyqt5 --config-settings --confirm-license= --verbose

https://www.youtube.com/@ComputerVisionEngineer/playlists

🔥  Main Kubectl Commands - K8s CLI 🔥
►  Get status of different components
►  create a pod/deployment
►  layers of abstraction
►  change the pod/deployment
►  debugging pods
►  delete pod/deployment
►  CRUD by applying configuration file

🔗 Links: 
- Git repo link of all the commands: https://bit.ly/3oZzuHY

🔥  K8s YAML Configuration File 🔥
►  3 parts of a Kubernetes config file (metadata, specification, status)
►  format of configuration file
►  blueprint for pods (template)
►  connecting services to deployments and pods (label & selector & port)
►  demo

🔗 Links:
- Git repo link: https://bit.ly/2JBVyIk

🔥 Demo Project 🔥
►  Deploying MongoDB and Mongo Express
►  MongoDB Pod
►  Secret
►  MongoDB Internal Service
►  Deployment Service and Config Map
►  Mongo Express External Service

🔗 Links:
- Git repo link: https://bit.ly/3jY6lJp

🔥  Organizing your components with K8s Namespaces 🔥
►  What is a Namespace?
►  4 Default Namespaces
►  Create a Namespace
►  Why to use Namespaces? 4 Use Cases
►  Characteristics of Namespaces
►  Create Components in Namespaces
►  Change Active Namespace

🔗 Links:
- Install Kubectx: https://github.com/ahmetb/kubectx#ins...

🔥  K8s Ingress explained 🔥
►  What is Ingress? External Service vs. Ingress
►  Example YAML Config Files for External Service and Ingress
►  Internal Service Configuration for Ingress
►  How to configure Ingress in your cluster?
►  What is Ingress Controller?
►  Environment on which your cluster is running (Cloud provider or bare metal)
►  Demo: Configure Ingress in Minikube
►  Ingress Default Backend
►  Routing Use Cases
►  Configuring TLS Certificate

🔗 Links:
- Git Repo: https://bit.ly/3mJHVFc
- Ingress Controllers: https://bit.ly/32dfHe3
- Ingress Controller Bare Metal: https://bit.ly/3kYdmLB

🔥  Helm - Package Manager 🔥
►  Package Manager and Helm Charts
►  Templating Engine
►  Use Cases for Helm
►  Helm Chart Structure
►  Values injection into template files
►  Release Management / Tiller (Helm Version 2!)

🔗 Links:
- Helm hub: https://hub.helm.sh/
- Helm charts GitHub Project: https://github.com/helm/charts
- Install Helm: https://helm.sh/docs/intro/install/

🔥  Persisting Data in K8s with Volumes 🔥
►  The need for persistent storage & storage requirements
►  Persistent Volume (PV)
►  Local vs Remote Volume Types
►  Who creates the PV and when?
►  Persistent Volume Claim (PVC)
►  Levels of volume abstractions
►  ConfigMap and Secret as volume types
►  Storage Class (SC)

🔗 Links:
- Git Repo: https://bit.ly/2Gv3eLi

🔥  Deploying Stateful Apps with StatefulSet 🔥
►  What is StatefulSet? Difference of stateless and stateful applications
►  Deployment of stateful and stateless apps
►  Deployment vs StatefulSet
►  Pod Identity
►  Scaling database applications: Master and Worker Pods
►  Pod state, Pod Identifier
►  2 Pod endpoints

🔥  K8s Services 🔥
►   What is a Service in K8s and when we need it?
►  ClusterIP Services
►  Service Communication
►  Multi-Port Services
►  Headless Services
►  NodePort Services
►  LoadBalancer Services
