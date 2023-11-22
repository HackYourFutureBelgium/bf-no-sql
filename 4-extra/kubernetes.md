# Kubernetes - Orchestrating Containerized Applications

## Overview

**Kubernetes** is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. It was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF). Kubernetes provides a robust and scalable infrastructure for deploying and managing containerized microservices.

## Prerequisites

Before diving into Kubernetes, ensure you have:

- A basic understanding of containers (Docker).
- Access to a Kubernetes cluster (local cluster, cloud-based cluster, or managed Kubernetes service).
- `kubectl` command-line tool installed.

## Key Concepts

- **Node:** A physical or virtual machine in the Kubernetes cluster where containers run.

- **Cluster:** A set of nodes grouped together.

- **Pod:** The smallest deployable unit in Kubernetes, representing a single instance of a running process.

- **Service:** An abstraction that defines a set of Pods and a policy to access them. It provides a stable IP address and DNS name.

- **ReplicaSet:** Ensures a specified number of replicas of a Pod are running.

- **Deployment:** Manages the deployment of a set of Pods. It provides declarative updates to applications.

- **ConfigMap:** Allows you to decouple environment-specific configuration from container images.

- **Secret:** Securely stores sensitive information, such as passwords or API keys.

- **Persistent Volume (PV) and Persistent Volume Claim (PVC):** Provide a way to decouple storage configuration from Pods.

- **Ingress:** Manages external access to services in a cluster, typically HTTP.

- **Namespace:** A way to divide cluster resources between multiple users.

## Kubernetes Architecture

Kubernetes follows a master-worker architecture:

- **Master Node:**

  - **Kube-apiserver:** Exposes the Kubernetes API.
  - **etcd:** Consistent and highly-available key-value store for all cluster data.
  - **Kube-controller-manager:** Enforces desired state for object types like Pods and Services.
  - **Kube-scheduler:** Assigns Pods to Nodes based on resource availability.

- **Worker Node:**
  - **Kubelet:** Ensures containers are running in a Pod.
  - **Kube-proxy:** Maintains network rules on nodes.

## Installation

Choose a method that suits your environment:

- **Local Cluster (Minikube):** A lightweight and easy-to-install Kubernetes distribution for development and testing.

  - [Minikube Installation](https://minikube.sigs.k8s.io/docs/start/)

- **Cloud-Based Cluster (Google Kubernetes Engine - GKE, Amazon EKS, Microsoft AKS):**
  - [GKE Quickstart](https://cloud.google.com/kubernetes-engine/docs/quickstart)
  - [EKS Getting Started](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html)
  - [AKS Quickstart](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough-portal)

## Kubectl - Kubernetes Command-Line Tool

- **Checking Cluster Information:**

  ```bash
  kubectl cluster-info
  ```

- **Checking Nodes:**

  ```bash
  kubectl get nodes
  ```

- **Checking Pods, Services, and Deployments:**
  ```bash
  kubectl get pods
  kubectl get services
  kubectl get deployments
  ```

## Deploying Applications

- **Creating a Deployment:**

  ```bash
  kubectl create deployment my-deployment --image=my-image
  ```

- **Scaling a Deployment:**

  ```bash
  kubectl scale deployment my-deployment --replicas=3
  ```

- **Updating a Deployment:**
  ```bash
  kubectl set image deployment/my-deployment my-container=new-image:tag
  ```

## Pods

- **Creating a Pod:**

  ```bash
  kubectl run my-pod --image=my-image
  ```

- **Checking Logs:**

  ```bash
  kubectl logs my-pod
  ```

- **Executing Commands in a Pod:**
  ```bash
  kubectl exec -it my-pod -- /bin/bash
  ```

## Services

- **Creating a Service:**

  ```bash
  kubectl expose deployment my-deployment --port=80 --target-port=8080 --type=LoadBalancer
  ```

- **Checking Service Information:**
  ```bash
  kubectl get services my-service
  ```

## ReplicaSets

- **Creating a ReplicaSet:**

  ```bash
  kubectl create replicaset my-replicaset --replicas=3 --image=my-image
  ```

- **Checking ReplicaSets:**
  ```bash
  kubectl get replicaset my-replicaset
  ```

## Deployments

- **Creating a Deployment:**

  ```bash
  kubectl create deployment my-deployment --image=my-image
  ```

- **Checking Deployments:**

  ```

  ```

bash
kubectl get deployments

````

## ConfigMaps and Secrets

- **Creating a ConfigMap:**
```bash
kubectl create configmap my-configmap --from-literal=key1=value1 --from-literal=key2=value2
````

- **Creating a Secret:**
  ```bash
  kubectl create secret generic my-secret --from-literal=username=user --from-literal=password=pass
  ```

## Persistent Volumes (PV) and Persistent Volume Claims (PVC)

- **Creating a Persistent Volume:**

  ```bash
  kubectl apply -f my-pv.yaml
  ```

- **Creating a Persistent Volume Claim:**
  ```bash
  kubectl apply -f my-pvc.yaml
  ```

## Ingress

- **Creating an Ingress:**
  ```bash
  kubectl apply -f my-ingress.yaml
  ```

## Namespaces

- **Creating a Namespace:**

  ```bash
  kubectl create namespace my-namespace
  ```

- **Switching to a Namespace:**
  ```bash
  kubectl config set-context --current --namespace=my-namespace
  ```

## Monitoring and Logging

- **Prometheus:** An open-source monitoring solution for collecting and querying metrics.

  - [Prometheus Documentation](https://prometheus.io/docs/introduction/overview/)

- **Grafana:** An open-source analytics and monitoring platform.

  - [Grafana Documentation](https://grafana.com/docs/grafana/latest/)

- **EFK Stack (Elasticsearch, Fluentd, Kibana):** A popular logging solution.
  - [Elasticsearch Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)
  - [Fluentd Documentation](https://docs.fluentd.org/)
  - [Kibana Documentation](https://www.elastic.co/guide/en/kibana/current/index.html)

## Scaling Applications

- **Horizontal Pod Autoscaler (HPA):** Automatically adjusts the number of Pods in a Deployment or ReplicaSet.

  - [HPA Documentation](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)

- **Cluster Autoscaler:** Automatically adjusts the size of a node pool.
  - [Cluster Autoscaler Documentation](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md)

## Upgrading Applications

- **Rolling Update:**
  ```bash
  kubectl set image deployment/my-deployment my-container=new-image:tag
  ```

## Rollbacks

- **Rolling Back a Deployment:**
  ```bash
  kubectl rollout undo deployment/my-deployment
  ```

## Security

- **Role-Based Access Control (RBAC):**

  - [RBAC Documentation](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

- **Pod Security Policies:**

  - [Pod Security Policies Documentation](https://kubernetes.io/docs/concepts/policy/pod-security-policy/)

- **Network Policies:**
  - [Network Policies Documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

## Kubernetes Ecosystem

- **Helm:** A package manager for Kubernetes applications.

  - [Helm Documentation](https://helm.sh/docs/)

- **Kustomize:** Customize Kubernetes manifests.

  - [Kustomize Documentation](https://kubectl.docs.kubernetes.io/pages/app_composition_and_decomposition/kustomize.html)

- **Istio:** A service mesh for Kubernetes.

  - [Istio Documentation](https://istio.io/latest/docs/)

- **Tekton:** A Kubernetes-native framework to build and deploy CI/CD pipelines.
  - [Tekton Documentation](https://tekton.dev/docs/)
