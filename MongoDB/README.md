## Deploying MongoDB - Lab 01

### Requirements

1. Install Operator, please refer to README.md in root directory. 

2. Cloud Manager account(Recommended)
  - Go to https://cloud.mongodb.com
  - Create Organization level API keys that will be required in later phase. 
  - Add Operator pod/worker node IP in the whitelist entry. 
  - Also note the organization ID. 


3. Ops Manager Instance(optional), if you already have Cloud Manager account prefer using that.  
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
- Update `om-connection/om-org-config.yaml` with OrgId and Project Name(this is the desired project name).
  - Apply this ConfigMap object
  ```
  kubectl apply -f om-connection/om-org-config.yaml
  ```
- Create an Org Level API Key in Ops Manager and update `om-connection/om-api-credentials.yaml` with public and private API keys.
  - Apply this secret object
  ```
  kubectl apply -f om-connection/om-api-credentials.yaml
  ```

### The MongoDB Folder has following CRDs(YAML) files for hands-on practice. 
- `replicaset-samples` - Contains sample replica-set CRDs.
    - `demo-replicaset.yaml` - The basic CRDs for plain/simple install of MongoDB.
    - `demo-replicaset-tls.yaml` - The TLS enabled deployment of MongoDB. 
    - `demo-replicaset-split-horizon.yaml` - The TLS enabled and Split horizon configured MongoDB for external connectivity use cases. 

- `certs` - Contain pre-generated certs if you do not wish to change the replicaset name(metadata.name) of the above CRDs.
  - ca-pem - contains CA Cert
  - demo-replicaset-{0,1,2}-pem - containes MongoDB certificates.
  - You may need to regenerate certificate for split horizon configuration as it has a specific DNS in generated certificate.
  - A quickest way to generate certificate is to use https://github.com/bhartiroshan/tlsgencer repo.
  - Clone the repo and just run like below.
    ```
    ./tlsgencer -server -host=server1.com,server2.com -cn=demo-replicaset
    ```
  - The certificate will be ready within seconds. Please refer to repo for more details. 

- `service-nodeport` - Contains nodeport service samples to expose the replica-set pods. 



