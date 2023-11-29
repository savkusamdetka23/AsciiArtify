# Analysis of local Kubernetes deployment tools and alternatives for AsciiArtify team

**AsciiArtify** is a software product for converting images to ascii-art using Machine Learning.I would like to present a Concept file for the team to advise with tools for the local development and testing system, considering Kubernetes-based options - minikube, kind and k3d (+Podman as alternative).


## Introduction
**minikube:** it implements a local Kubernetes cluster on macOS, Linux, and Windows. minikube's primary goals are to be the best tool for local Kubernetes application development and to support all Kubernetes features that fit.

**kind (Kubernetes in Docker):** is a tool for running local Kubernetes clusters using Docker container “nodes”. kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

**k3d (k3s in Docker):** is a lightweight wrapper to run k3s (Rancher Lab’s minimal Kubernetes distribution) in docker. It provides an easy way to spin up a K3s cluster for local development and testing. k3d makes it very easy to create single- and multi-node k3s clusters in docker, e.g. for local development on Kubernetes

**Podman (as an alternative):** by using it, you can locally create Kubernetes pods from containers and then generate Kubernetes YAML from Pods for the further deployment to k8s. 

## Features

| Feature                 	| minikube                               	| kind                                                     	| k3d                                                  	| Podman                                   	|
|-------------------------	|----------------------------------------	|----------------------------------------------------------	|------------------------------------------------------	|------------------------------------------	|
| Supported OS            	| Cross-platform (Linux, macOS, Windows) 	| Cross-platform (Linux, macOS, Windows)                   	| Cross-platform (Linux, macOS, Windows)               	| Linux, macOS, Windows (with limitations) 	|
| Supported Architectures 	| AMD64, ARM64                           	| AMD64                                                    	| AMD64                                                	| AMD64, ARM64                             	|
| Automation Capability   	| Good automation support                	| Supports automation using Kubernetes manifests           	| Supports automation using K3s configuration          	| Limited, more manual setup required      	|
| Additional Features     	| Have addons for extra functionality         	| Multiple CNI plugins, can be extended with other tools   	| K3s can use addons for additional functionality              	| Daemonless, rootless container engine    	|
| Monitoring & Management 	| Supports addons for monitoring         	| Limited built-in tools, usually leverages external tools 	| Limited built-in tools, focuses on lightweight setup 	| Monitoring through external tools        	|

### Licensing considerations
The Docker Engine, which includes the Docker daemon, client, and container runtime, is open source and governed by the Apache License 2.0. However, Docker also offers a commercial product called Docker Enterprise that includes additional features and support.

The potential licensing concerns or risks related to Docker are more likely associated with the use of Docker Enterprise or other commercial Docker products rather than the open-source Docker Engine. Here are some considerations:
 1.  **minikube :** it can use various container runtimes, including Docker. Docker Desktop, is free for personal use like local development but may have licensing considerations for business or enterprise use. We need to be  sure to review Docker's licensing terms if we decide to use Docker Desktop in a business context.
    
2.  **kind :** it just interacts with the Kubernetes API and doesn't involve Docker in any way that triggers additional licensing concerns.
    
3.  **k3d:** is designed to work with lightweight Kubernetes clusters using K3s, and do not directly rely on Docker licensing.
    
4.  **Podman:** is a daemonless, container engine. It doesn't rely on Docker daemon, and its primary focus is on providing a container runtime without requiring a daemon. So Podman is governed by open-source licenses.

## Advantages and Disadvantages:

| **Tool**      | **Advantages**                                                                                                    | **Disadvantages**                                                                                              |
|---------------|-------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| **minikube**  | - Good documentation and community support.<br/> - Suitable for local development and testing.                                                                      | - Slower startup due to VM initialization.<br/> - Resource-intensive compared to other options.               |
| **kind**      | - Lightweight and fast startup.<br/> - Excellent for local development and testing.                                                                                | - Limited built-in monitoring tools.<br/> - Documentation can be less extensive.                               |
| **k3d**       | - Fast startup with K3s (lightweight Kubernetes).<br/> - Good support for K3s addons.                             | - Documentation could be more comprehensive.            |
| **Podman**    | - Daemonless, rootless container engine.<br/> - Simplicity and ease of use.                                     | - Not primarily designed for Kubernetes clusters. <br/> - require a deeper understanding of containerization and Linux operating systems.                               |


##  Demonstration

#### k3d :
Сonsidering the speed, ease of use and low entry threshold, it is recommended to use k3d. Let me shot you how fast you can locally deploy an app by using k3d:

    k3d cluster create AsciiArtify
    export KUBECONFIG="$(k3d kubeconfig write AsciiArtify)"
    kubectl create deployment hello-world --image=nginx
    kubectl expose deployment hello-world --type=LoadBalancer --port=80
    kubectl get svc -w

  [asciicast recorded gif](623914.gif)

## Conclusions

###   **minikube:**
    
    -   Suitable for local Kubernetes development and testing.
    -   Recommended for scenarios requiring a full-featured Kubernetes cluster on a single machine.

###   **kind:**
    
    -   Ideal for lightweight, fast local Kubernetes development.
    -   Recommended for rapid testing and development where resource constraints are a concern.

###   **k3d:**
    
    -   Excellent for lightweight local Kubernetes development with a focus on simplicity.
    -   Recommended for scenarios where K3s is preferred.

###   **Podman:**
    
    -   Suited for scenarios where a daemonless, rootless container engine is essential.
    -   Recommended for simpler container workloads without the need for a full Kubernetes cluster.
