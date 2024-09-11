# Manual setup

## Initialization

```bash
minikube start --driver=virtualbox
alias k="kubectl"
k create deployment k8s-web-hello --image=tiagospeckart/k8s-web-hello
```

## Cluster IP service (default)

```bash
k expose deployment k8s-web-hello --port=3001
k get svc # Get Cluster-IP
minikube ssh
curl <k8s-web-hello Cluster-IP>:3001
exit
k scale deployment k8s-web-hello --replicas=4 
k get pods -o wide
```

## NodePort service

Exposes minikube IP to be reachable externally

```bash
k delete svc k8s-web-hello
k expose deployment k8s-web-hello --type=NodePort --port=3001
k get svc # Notice the type of the service, copy exposed port
minikube ip # Use this IP + exposed port
```

Node server is reachable from minikubeIp:randomlyExposedPort
With replicas, each refresh will show a different pod being used due to kubernetes load balancing

To reach the service more easily, run
```bash
minikube service k8s-web-hello
# or 
minikube service k8s-web-hello --url
```

## Load Balancer service

```bash
k delete svc k8s-web-hello
k expose deployment k8s-web-hello --type=LoadBalancer --port=3001
k get svc # External-IP is <pending>, it's normal. This is used by cloud providers
```

Previous commands from NodePort service are valid, you can connect externally using miniku ip, or run `minikube service k8s-web-hello`

## Updating image from deployment - Rolling update

```bash
k set image deployment k8s-web-hello k8s-web-hello=tiagospeckart/k8s-web-hello:2.0.0
k rollout status deploy k8s-web-hello
```