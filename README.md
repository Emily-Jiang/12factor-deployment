# 12factor-deployment

This repository contains an example deployment.yml for deploying 12factor-app-a and 12factor-app-b on Kubernetes

## Deploying to Minikube

1. Install and set up [Minikube][minikube] and [kubectl][kubectl]
1. Checkout this repository, 12factor-app-a and 12factor-app-b
1. Run `minikube start` if minikube is not already started
1. Run `eval $(minikube docker-env)` to set up your docker environment to connect to minikube
    * This only affects the current terminal. You must run this command for each terminal where you're going to build a docker image.
1. Change to the `12factor-app-a` directory and run `mvn package -P docker-image`. This will build the app and the docker image.
1. Change to the `12factor-app-b` directory and run `mvn package -P docker-image`. This will build the app and the docker image.
1. Change to the directory for this repository and run `kubectl apply -f deployment.yml`
    * This should deploy and start two instances of each app and expose service A on port 30080 on the minikube IP address
    * You can run `kubectl get pods` to watch your containers starting
1. Run `minikube ip` to get the minikube IP address
1. Visit `http://<minikube ip>:30080/demo/a` to see the response from service A

[minikube]: https://kubernetes.io/docs/tasks/tools/install-minikube/
[kubectl]: https://kubernetes.io/docs/tasks/tools/install-kubectl/
