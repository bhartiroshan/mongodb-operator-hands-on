## Operator Handson Lab

### Deploying MongoDB - Lab 01
### Requirements
- Kubernetes Cluster
You can get access to Openshift K8s Cluster(https://okd-ts-snkxg.mongodbstitch.com/). You need to connect to any VPN to access this cluster. Please refer to [this notification](https://groups.google.com/a/10gen.com/g/ts/c/ORTO-WmLE8A). 

- Ops Manager Instance
  - For Testing purpose you can spin up an EC2 instance and install Ops Manager. 
  - For quick lab setup, please refer to repo https://github.com/bhartiroshan/om. 
  - Launch Amazon EC2 instance and while launching provide below in EC2 user data script. 
  ```
    #!/bin/bash
    yum install -y git
    git clone https://github.com/bhartiroshan/om.git ~/om
    cd ~/om
    ./om init --platform=amazon
    ./om install --config=om-config.json --version=4.4.7 --username={username} --password={password}
  ```
  - For more details refer to the github repo. 
  - Remember to terminate the instance after testing. 

- Install MongoDB Kubernetes Operator
    1. Clone the MongoDB Kubernetes Operator git repository
    a. git clone https://github.com/mongodb/mongodb-enterprise-kubernetes.git :

    2. Install the CRDs(Custom Resource Definitions), it allows Kubernetes to understand Custome Objects like MongoDB OpsManager
    a. kubectl create namespace mongodb :
    b. kubectl apply -f mongodb-enterprise-kubernetes/crds.yaml :
    c. kubectl get crd : # Verify CRDs are installed

    3. Install the Operator
    a. kubectl apply -f mongodb-enterprise-kubernetes/mongodb-enterprise.yaml :
    b. kubectl get pods : # verify Operator pod is running 
