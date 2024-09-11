# Kubernetes Hello World

Hello world with kubernetes from [FreeCodeCamp Kubernetes Course - Full Beginners Tutorial](https://www.youtube.com/watch?v=d6WC5n9G_sM)

## Installation

### Required software

- VirtualBox (or any virtualization or compatible container engine)
- Minikube
- Docker

### Running with configuration files

```bash
minikube start --driver=virtualbox
alias k="kubectl"
k apply -f deployment.yml 
k apply -f service.yml 
```

### Running proxied nginx

```bash
k apply -f k8s-web-to-nginx.yaml -f nginx.yaml
```

## Changing container engine of minikube

```bash
minikube status
minikube stop
minikube delete
k8s minikube start --driver=virtualbox --container-runtime=cri-o # or containerd
```