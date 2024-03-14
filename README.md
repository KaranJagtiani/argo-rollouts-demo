# Argo Rollouts Demo

This repository contains demo projects for implementing Blue-Green and Canary release strategies using Argo Rollouts in a Kubernetes environment. The demos illustrate how to leverage Argo Rollouts for advanced deployment strategies to ensure seamless, safe software releases.

## Prerequisites

Before proceeding with the demos, ensure you have the following tools installed:

- **Docker**: Required for creating containerized applications. [Installation Guide](https://docs.docker.com/engine/install/)
- **Kind (Kubernetes in Docker)**: Used for running local Kubernetes clusters using Docker container "nodes". [Installation Guide](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)
- **Kubectx**: A utility to manage and switch between kubectl contexts. [Installation Guide](https://github.com/ahmetb/kubectx#installation)
- **Argo Rollouts Plugin**: A plugin for managing and visualizing rollouts.[Installation Guide](https://argoproj.github.io/argo-rollouts/installation/#kubectl-plugin-installation)

## Setup

To set up your environment for the Argo Rollouts demos, follow these steps:

1. Create a Kubernetes cluster using Kind:

    ```bash
    kind create cluster --name=argo-rollouts-demo
    ```

2. Switch to the newly created cluster context:

    ```bash
    kubectx kind-argo-rollouts-demo
    ```

## Install Argo CD Into the Kubernetes Cluster

    ```bash
    kubectl create namespace argo-rollouts

    kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml
    ```

## Blue-Green Deployment Demo

The Blue-Green deployment strategy involves running two versions of an application (blue and green) and switching traffic between them. This demo illustrates how to implement a Blue-Green deployment using Argo Rollouts.

1. Apply the green service:

    ```bash
    kubectl apply -f blue-green/01-green-service.yaml
    ```

2. Apply the blue service:

    ```bash
    kubectl apply -f blue-green/02-blue-service.yaml
    ```

3. Deploy the Argo Rollout:

    ```bash
    kubectl apply -f blue-green/03-argo-rollout.yaml
    ```

4. To monitor the rollout:

    ```bash
    kubectl argo rollouts get rollout nginx-rollout
    ```

5. Access the Argo Rollouts dashboard:

    ```bash
    kubectl argo rollouts dashboard
    ```

    Open your browser and navigate to `http://localhost:3100/rollouts` to view the rollout status.

## Canary Release Demo

The Canary release strategy allows you to roll out changes gradually to a small subset of users before rolling it out to the entire infrastructure. This demo demonstrates how to perform a Canary release using Argo Rollouts.

1. Apply the service:

    ```bash
    kubectl apply -f canary-release/01-service.yaml
    ```

2. Deploy the Argo Rollout:

    ```bash
    kubectl apply -f canary-release/02-argo-rollout.yaml
    ```

## Repository Structure

- `LICENSE`: The license file.
- `README.md`: This README file.
- `blue-green/`: Contains files for the Blue-Green deployment demo.
- `canary-release/`: Contains files for the Canary release demo.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
