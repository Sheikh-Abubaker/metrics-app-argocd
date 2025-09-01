 Metrics App

This project demonstrates deploying a simple counter-based application using Kubernetes, Helm, and ArgoCD with NGINX Ingress in a local KIND cluster.

## 🚀 Prerequisites

Make sure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/)
- [KIND](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Helm](https://helm.sh/docs/intro/install/)

---

## 📦 Project Structure

```bash
.
├── charts/
│   └── metrics-app/         # Helm chart for the application
├── argocd/
│   └── metrics-app.yaml     # ArgoCD Application manifest
└── README.md                # Readme file
````

---

## 🧪 Quick Start

- Start Docker and create KIND Cluster

    ```bash
    kind create cluster --name sre-assignment
    ```

- Install NGINX Ingress Controller

    Create ```ingress-nginx``` namespace to install NGINX Ingress Controller:
    ```bash
    kubectl create namespace ingress-nginx
    ```

    Pull the chart sources:

    ```bash
    helm pull oci://ghcr.io/nginx/charts/nginx-ingress --untar --version 2.1.0
    ```

    Change your working directory to nginx-ingress:

    ```bash
    cd nginx-ingress
    ```

    Install the chart in ```ingress-nginx``` namespace :

    ```bash
    helm install nginx-ingress . -n ingress-nginx
    ```


- [Install Argo CD](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

- [Install Argo CD CLI](https://argo-cd.readthedocs.io/en/stable/cli_installation/#installation)

- [Access The Argo CD API Server](https://argo-cd.readthedocs.io/en/latest/getting_started/#3-access-the-argo-cd-api-server)

- [Login Using The CLI](https://argo-cd.readthedocs.io/en/latest/getting_started/#4-login-using-the-cli)

---

## 🛠 Deploy the App with ArgoCD

- Clone this repository

    Install [git](https://git-scm.com/downloads) (if not already)

    ```bash
    git clone https://github.com/Sheikh-Abubaker/sre-assignment.git
    ```

    Change your working directory to sre-assignment:

    ```bash
    cd sre-assignment
    ```

- Apply the ArgoCD Application

    ```bash
    kubectl apply -f argocd/metrics-app.yaml
    ```

- [Sync (Deploy) The Application](https://argo-cd.readthedocs.io/en/stable/getting_started/#7-sync-deploy-the-application)

---

## 🔁 Access the App

- Retrieve NGINX Ingress Controller service:

    ```bash
    kubectl get svc -n ingress-nginx
    ```

    Excpected output
    ```bash
    NAME                       TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
    nginx-ingress-controller   LoadBalancer   10.96.218.123   <pending>     80:30141/TCP,443:30595/TCP   6h20m
    ```


- Port forward to the NGINX Ingress Controller:

    ```bash
    kubectl port-forward -n ingress-nginx svc/nginx-ingress-controller 8085:80
    ```

- Access Using curl or visit [webpage](http://localhost:8085/counter):
    ```bash
    curl http://localhost:8085/counter
    ```


- Each call should return an incremented counter value.

    ```bash
    for i in $(seq 0 20); do time curl localhost:8085/counter; done
    Counter value: 1
    real    0m0.191s
    user    0m0.003s
    sys     0m0.007s
    Counter value: 2
    real    0m0.012s
    user    0m0.004s
    sys     0m0.000s
    Counter value: 3
    real    0m0.014s
    user    0m0.004s
    sys     0m0.000s
    Counter value: 4
    real    0m0.035s
    user    0m0.006s
    sys     0m0.001s
    Counter value: 5
    real    0m0.026s
    user    0m0.000s
    sys     0m0.008s
    Counter value: 6
    real    0m0.022s
    user    0m0.000s
    sys     0m0.008s
    Counter value: 7
    real    0m0.026s
    user    0m0.000s
    sys     0m0.010s
    Counter value: 8
    real    0m0.028s
    user    0m0.008s
    sys     0m0.001s
    Counter value: 9
    real    0m0.046s
    user    0m0.007s
    sys     0m0.008s
    Counter value: 10
    real    0m0.066s
    user    0m0.019s
    sys     0m0.001s
    Counter value: 11
    real    0m0.074s
    user    0m0.000s
    sys     0m0.019s
    Counter value: 12
    real    0m0.093s
    user    0m0.011s
    sys     0m0.012s
    Counter value: 13
    real    0m0.133s
    user    0m0.016s
    sys     0m0.007s
    Counter value: 14
    real    0m0.091s
    user    0m0.000s
    sys     0m0.016s
    Counter value: 15
    real    0m0.103s
    user    0m0.007s
    sys     0m0.015s
    Counter value: 16
    real    0m31.614s
    user    0m0.019s
    sys     0m4.044s
    Counter value: 17
    real    0m0.152s
    user    0m0.000s
    sys     0m0.016s
    Counter value: 18
    real    0m0.027s
    user    0m0.000s
    sys     0m0.008s
    Counter value: 19
    real    0m0.057s
    user    0m0.007s
    sys     0m0.001s
    Counter value: 20
    real    0m0.022s
    user    0m0.006s
    sys     0m0.001s
    Counter value: 21
    real    0m0.027s
    user    0m0.007s
    sys     0m0.001s
    ```

---
