## Operator Handson Lab

### Requirements
- Kubernetes Cluster
You can get access to Openshift K8s Cluster(https://okd-ts-snkxg.mongodbstitch.com/). You need to connect to any VPN to access this cluster. Please refer to [this notification](https://groups.google.com/a/10gen.com/g/ts/c/ORTO-WmLE8A). 

- Install MongoDB Kubernetes Operator
  1. Clone the MongoDB Kubernetes Operator git repository
    - git clone https://github.com/mongodb/mongodb-enterprise-kubernetes.git 

  2. Install the CRDs(Custom Resource Definitions), it allows Kubernetes to understand Custome Objects like MongoDB OpsManager
    - kubectl create namespace mongodb 
    - kubectl apply -f mongodb-enterprise-kubernetes/crds.yaml 
    - kubectl get crd : # Verify CRDs are installed

  3. Install the Operator
    -  kubectl apply -f mongodb-enterprise-kubernetes/mongodb-enterprise.yaml 
    -  kubectl get pods : # verify Operator pod is running 
