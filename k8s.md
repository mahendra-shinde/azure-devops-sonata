Individual container is NOT reliable
  Created/Destroyed/Start/Stop many times

Containers need MANUAL scaling

No Load Balancing

No Service Discovery


Container Orchestration Engines 
 -- Self Heal
 -- Scale Auto
 -- Load Balancing
 -- Service Discovery


 Kubernetes  ( Work with Docker, RKT, LXC & LXD ) (Windows)
 Docker Swarm (Work with Docker) (Windows)
 DC/OS with Apache Mesos (Work with RKT, LXC, LXD, Docker??? )
 
 Kubernetes:
     Docker Desktop (Single Node)	
     Minikube (Single node)
     AKS (Cloud)

 AKS Creation:
	# Create a resource group
	$ az group create -n my_aks -l southeastasia
	# Create aks
	$ az aks create -n aks12001 -g my_aks --generate-ssh --node-count=2

	# Get AKS Credentials (YAML)
	$ az aks get-credentials -n aks12001 -g my_aks
	
	# Download to local system
	$ download .kube/config

	Download kubectl on local machine from URL:
	https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/windows/amd64/kubectl.exe

	Once downloaded, Keep kubectl in directory C:\kube
	From command prompt use command:
	$ set path=%path%;c:\kube
	$ kubectl cluster-info




