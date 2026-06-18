
               Architecture of Kubernetes:
 What is Kubernetes and Why is it Used?
Kubernetes is a container orchestration platform.
The purpose of using Kubernetes is to solve the problems we face with Docker containers, such as Auto Healing, Auto Scaling, Load Balancing, and meeting Enterprise-level standards.
Let's try to understand the architecture of Kubernetes:
Kubernetes is installed in a cluster architecture.
A Kubernetes cluster is divided into two components:
1. Control Plane (Master Node)
2. Data Plane (Worker Node)

1) Control Plane:The Control Plane is also called the Master Node.
The Control Plane consists of the following components:
a) API Server
b) Scheduler
c) ETCD
d) Controller Manager
e) CCM (Cloud Controller Manager)
a) API Server:
The API Server is generally used to perform actions received from the external world.
When a user tries to access an application using an IP address, the API Server receives the request, validates it, and performs the required action. It acts as the entry point for all communications within the Kubernetes cluster.
b) Scheduler:
The Scheduler is responsible for deciding on which Pod/Container a request should be executed based on the available resources and requirements.
It schedules workloads to the appropriate Worker Node after receiving information from the API Server.
c)ETCD: 
ETCD is used as a backup storage system for the entire cluster.
It is a distributed key-value store that maintains all cluster information, including Kubernetes objects, configurations, and metadata. ETCD acts as the source of truth for the Kubernetes cluster.
d)Controller Manager:
Kubernetes has multiple Pods and Controllers. The Controller Manager is responsible for ensuring that all controllers are working properly, running, and healthy.
For example, suppose the ReplicaSet (which is a controller) is configured with a replica count of 3 in the YAML file. When the cluster is created, Kubernetes ensures that 3 Pods are always running.
If one of the Pods goes down or gets deleted, the ReplicaSet automatically creates a new Pod through the Controller Manager to maintain the desired state specified in the YAML file.
In short, the Controller Manager continuously compares the actual state with the desired state and takes corrective actions whenever required.

e)CCM (Cloud Controller Manager):
Kubernetes can run on cloud platforms such as EKS, AKS, and GKE.
The Cloud Controller Manager (CCM) allows Kubernetes to interact with cloud provider services. Cloud providers write and maintain the code required for Kubernetes integration.
For example, if a DevOps Engineer wants to deploy an application on AWS, the AWS-specific integration provided to Kubernetes allows the CCM to automatically create an Elastic Load Balancer (ELB).
This Load Balancer provides a Public IP Address through which users from the external world can access the application.

2) Data Plane:
The Data Plane is also known as the Worker Node in Kubernetes architecture.
It consists of the following components:
a) Kubelet
b) Kube-Proxy
c) Container Runtime

a)Kubelet :
Kubelet is responsible for ensuring that the Containers are running, healthy, and available in the desired quantity.If a Container or Pod becomes unhealthy or is deleted, Kubelet sends the status information to the API Server. The API Server then communicates with the appropriate Controller, which creates new Pods if required.
Kubelet also ensures that Containers are started, stopped, and monitored as needed to maintain the desired state defined in the YAML file.

b)Kube-Proxy:
Kube-Proxy provides networking for each Node in the Kubernetes cluster.
It is responsible for:
* Providing network communication between Pods and Services.
* Load balancing traffic across Pods.
* Managing network rules and routing.
* Updating IP tables whenever Pods are created or deleted.
Kube-Proxy helps ensure that requests are routed correctly to the appropriate Pods.
c)Container Runtime:
To run containers in a Kubernetes cluster, a Container Runtime is required.
Examples include:
* Docker Shim (deprecated)
* containerd
* CRI-O
The Container Runtime is responsible for running and managing containers on Worker Nodes. It pulls container images, starts containers, stops containers, and manages their lifecycle.

Summary: A Kubernetes cluster consists of:
1)Control Plane (Master Node)
* API Server
* Scheduler
* ETCD
* Controller Manager
* Cloud Controller Manager (CCM)
2) Data Plane (Worker Node)
* Kubelet
* Kube-Proxy
* Container Runtime

Together, these components help Kubernetes provide features such as Auto Healing, Auto Scaling, Load Balancing, and efficient management of containerized applications.
 
Kubelet
Kube-proxy
Container Run Time
API Server
Scheduler
ETCD
Controll Manager
CCM(Cloud Control Manager)
                   Control Plane                                Data Plane
                              Fig. Kubernetes Architecture.