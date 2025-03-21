# Installing and setting up Kubernetes Minikube, and deploying Image from Docker Hub

## Install Minikube in Linux

#### Install required packages

- Update the package information on the system by entering the following command:
```bash
sudo apt update
```
![1](https://github.com/user-attachments/assets/cd2810c4-b710-44b8-be4a-2a75f8efe6e9)

- Install `curl` and `apt-transport-https`
```bash
sudo apt install curl apt-transport-https
```
![2](https://github.com/user-attachments/assets/00f8e2c2-1e0c-4450-9bba-28a2b0bd96ee)


#### Download Minikube Binary

- Use curl to download the latest Minikube binary:
```bash
curl -O https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
![3 curl](https://github.com/user-attachments/assets/d8e898e3-7193-4b42-9bd3-ed224ce929c9)

- Copy the downloaded file and store it in the /usr/local/bin/ directory:
```bash
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
```

#### Enable Minikube Binary Execution

- By default, binaries do not have the permission to execute. Give the execute permission to the Minikube binary using the chmod command:
```bash
sudo chmod 755 /usr/local/bin/minikube
```
- Verify the installation by checking the Minikube version:
```bash
minikube version
```
![4 version](https://github.com/user-attachments/assets/99b4b77f-234f-4723-a0a2-518aa9886b99)

- The output displays the software version number.

#### Install kubectl

- Kubectl is the official command line tool for Kubernetes, which provides an interface for cluster deployment and management. Ubuntu has a kubectl snap package that can be installed by typing:
```bash
sudo snap install kubectl --classic
```
![2](https://github.com/user-attachments/assets/247b6be6-e0f9-4690-9007-c5335d048148)

- Alternatively, follow the steps below to download and install the kubectl binary directly from the maintainer:
  - Download kubectl with the following command:
  ```bash
  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
  ```
  ![3](https://github.com/user-attachments/assets/3552d279-02a2-4354-b7b1-0909f03dcd2d)

  - Make the binary executable by typing:
  ```bash
  chmod +x ./kubectl
  ```
  - Move the binary to the path with the following command:
  ```bash
  sudo mv ./kubectl /usr/local/bin/kubectl
  ```

#### Start Minikube

- Start Minikube by running the command below:
```bash
minikube start
```
![start](https://github.com/user-attachments/assets/0ec0b437-70f9-452e-8fd4-6e161e507559)

- Once Minikube finishes initialization, the output shows the confirmation message, and the shell prompt reappears.
Minikube initialization complete.

#### Common Minikube Commands

- See the status of the Minikube container, the cluster, and the core Kubernetes components:
```bash
minikube status
```
![status](https://github.com/user-attachments/assets/df7bb9d8-b681-43de-a54c-41950c7f1db0)

- Display a list of installed Minikube addons:
```bash
minikube addons list
```
![addons list](https://github.com/user-attachments/assets/6e80511e-55ee-4e09-aa51-3423a169fe74)

- Enable an addon:
```bash
minikube addons enable dashboard
```
![dashboard](https://github.com/user-attachments/assets/067d1b3f-f2be-4cc3-987a-e9635c6a3f03)

```bash
minikube addons enable ingress
```
![ingress](https://github.com/user-attachments/assets/dfa522a7-847c-48ea-8bee-efbc792445ee)

- Stop running the Minikube cluster:
```bash
minikube stop
```
![stop](https://github.com/user-attachments/assets/fabe7a09-ed5c-4e72-bda1-9395ce7bf712)

- Delete the Minikube cluster:
```bash
minikube delete
```
![delete](https://github.com/user-attachments/assets/031db394-1840-4b55-92a9-55404d0a2485)


#### Access Minikube Dashboard

- Run the command below to enable and access the Minikube dashboard:
```bash
minikube dashboard
```
![dashboard final](https://github.com/user-attachments/assets/54ecc507-46a3-4ce3-a077-eaa778bfc7ff)

- Alternatively, to access the dashboard directly via the browser, obtain the dashboard’s IP address:
```bash
minikube dashboard --url
```
![Screenshot from 2025-03-21 12-48-49](https://github.com/user-attachments/assets/466b9f4f-3da0-4cab-b181-d5817c429b52)

- In the browser the kuburnetes dashboard will become visible like below:

![final](https://github.com/user-attachments/assets/40be204b-1003-4177-8ccf-586dbdbf8265)


