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

- In the browser the Minikube dashboard will become visible like below:

![final](https://github.com/user-attachments/assets/40be204b-1003-4177-8ccf-586dbdbf8265)

## Deploy Image from Docker Hub

#### Change file content of Dockerfile in github repository of day2 task

- Previous file content looks like below:
```bash
EXPOSE 3001
```
![git dockerfile before](https://github.com/user-attachments/assets/ef105ef3-e573-4f79-b825-3e7c08ad5d1f)

- Modify the port address from 3001 to 80 as follows:
```bash
EXPOSE 80
```
![git dockerfile after](https://github.com/user-attachments/assets/1b233a8b-5113-44ae-a753-8f2f59a5b85e)

- Then give 'Build now' in corresponding Jenkins pipeline:

![jenkins build 8 after edit dockefile](https://github.com/user-attachments/assets/e82c0333-7c48-49c5-a3b3-a602e949c3f0)

#### Create directory for Docker in Local Machine

- Create the repository 'docker'
```bash
mkdir docker
```
- Make 'docker' the current working directory
```bash
cd docker
```
- Install Node Package Manager (npm) in the terminal
```bash
sudo apt install npm
```
![sudo apt install npm](https://github.com/user-attachments/assets/23cda6af-7da0-4a42-ba08-e9c5f84052a1)

- Execute the following command to initialize a json file
```bash
npm init -y
```
![npm init y](https://github.com/user-attachments/assets/ae68f3e2-b8aa-4338-8d2d-3bf176348e53)

- Go to Dockerhub in browser and make sure the tag 'latest' exists
![docker hub tag latest](https://github.com/user-attachments/assets/9a5f1371-d990-4072-844b-d36ef1f6e01e)

- Now navigate back to terminal and build the docker image
```bash
docker build -t naghulpranavkk/docker:latest .
```
![docker build t](https://github.com/user-attachments/assets/c6708604-105f-4210-9dac-6da79fc1c427)
