## Deploying MongoDB - Lab 01

### Requirements

- Install Operator, please refer to README.md in root directory. 

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

### Install MongoDB

### Prerequisites:
- Creata a ConfigMap which holds Organization related information where Operator managed deployment will be place. 
- Update `om-org-config.yaml` with OrgId and Project Name(this is the desired project name).
- Create an Org Level API Key in Ops Manager and update `om-api-credentials.yaml` with public and private API keys.
- Apply this secret object
```
kubectl apply -f om-api-credentials.yaml
```

### The MongoDB Folder has following CRDs(YAML) files for hands-on practice. 
- demo-replicaset.yaml - The basic CRDs for plain/simple install of MongoDB.
- demo-replicaset-tls.yaml - The TLS enabled deployment of MongoDB. 
- demo-replicaset-split-horizon.yaml - The TLS enabled and Split horizon configured MongoDB for external connectivity use cases. 


