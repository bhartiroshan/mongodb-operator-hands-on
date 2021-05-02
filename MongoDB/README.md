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
