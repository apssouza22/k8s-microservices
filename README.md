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
* Visite https://github.com/apssouza22/istio-and-minikube

## Useful commands

* Getting the Ingress gateway service details
`kubectl get svc istio-ingressgateway -n istio-system`

* Add into the /etc/hosts the minikube_ip store.local.dev (`minikube ip` to get the Minikube  Ip)
* Access the gateway on https://ingress.local/



## Debugging
You should be able to acesse store straight by the ip.
Using the minikube ip + the service port
