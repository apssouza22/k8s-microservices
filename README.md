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
* Start a local k8s cluster `minikube start --cpus 4 --memory 12192`
* Enable Ingress `minikube addons enable ingress` 
* Start the application container `cd kubernetes && ./kubectl-apply.sh`
* Install Helm https://github.com/helm/helm#install
* Install Istio

```
export ISTIO_VERSION=1.3.0
curl -L https://git.io/getLatestIstio | sh -
ln -sf istio-$ISTIO_VERSION istio
export PATH=~/istio/bin:$PATH

# Create a namespace to Istio
kubectl create namespace istio-system

cd ~/istio-$ISTIO_VERSION
# Install the Istio CRDs
helm template install/kubernetes/helm/istio-init --name istio-init --namespace istio-system | kubectl apply -f -

# Run this to verify all CRDs are installed. It should output 23 for this version of Istio.
kubectl get crds -n istio-system | grep 'istio.io\|certmanager.k8s.io' | wc -l

# Install the Istio demo set up so that we get Grafana, Jaeger & Kiali set up as well.
# For production, use the Istio default setup. Refer https://istio.io/docs/setup/kubernetes/install/helm/
helm template install/kubernetes/helm/istio --name istio --namespace istio-system \
    --values install/kubernetes/helm/istio/values-istio-demo.yaml | kubectl apply -f -

```
* Wait for the pods to run, these will be deployed to the istio-system namespace.

`kubectl get pods -n istio-system -w`

*Getting the Ingress gateway service details
`kubectl get svc istio-ingressgateway -n istio-system`

* Use the script below to set the GATEWAY environment variable we will be using to access the services.
```
export INGRESS_HOST=$(minikube ip)
export INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}')
export GATEWAY=$INGRESS_HOST:$INGRESS_PORT
```

* Add into the /etc/hosts the minikube_ip store.local.dev (`minikube ip` to get the Minikube  Ip)
* Access the gateway on https://ingress.local/

## Debugging
You should be able to acesse store straight by the ip.
Using the minikube ip + the service port
