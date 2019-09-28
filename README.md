# The state of the art in microservices
*** This is a working in progress project

Basically we will migrate this project from Netflix OOS to Kubernates
This project will contain:
- Centralized authentication (JWT)
- Centralized log with ELK
- Centralized monitoring with Prometheus 
- Infrastructure management with Kubernates
- Service mesh with Istio
- Microservices communication with GRPC
- Continuous integration
- Event sourcing 
- Front-end with Angular 


## How to use
* Install Minikube
* Start a local k8s cluster `minikube start --cpus 4 --memory 8192` 
* `cd kubernates && ./kubectl-apply.sh`
* Add into the /etc/hosts the minikube_ip store.local.dev (`minikube ip` to get the Minikube  Ip)
* Access the gateway on https://ingress.local/
* Install Helm https://github.com/helm/helm#install

## Debugging
You should be able to acesse store straight by the ip.
Using the minikube ip + the service port
