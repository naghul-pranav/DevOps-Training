# Installing and setting up Kubernetes Minikube, and deploying Image from Docker Hub

## Install Minikube in Linux

#### Install required packages

- Update the package information on the system by entering the following command:
```bash
sudo apt update
```
- Install `curl` and `apt-transport-https`
```bash
sudo apt install curl apt-transport-https
```

#### Download Minikube Binary

- Use curl to download the latest Minikube binary:
```bash
curl -O https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
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
- The output displays the software version number.

#### Install kubectl

- Kubectl is the official command line tool for Kubernetes, which provides an interface for cluster deployment and management. Ubuntu has a kubectl snap package that can be installed by typing:
```bash
sudo snap install kubectl --classic
```
- Alternatively, follow the steps below to download and install the kubectl binary directly from the maintainer:
  - Download kubectl with the following command:
  ```bash
  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
  ```
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
- Once Minikube finishes initialization, the output shows the confirmation message, and the shell prompt reappears.
Minikube initialization complete.

#### Common Minikube Commands

- See the status of the Minikube container, the cluster, and the core Kubernetes components:
```bash
minikube status
```
- Display a list of installed Minikube addons:
```bash
minikube addons list
```
- Enable an addon:
```bash
minikube addons enable dashboard
```
```bash
minikube addons enable ingress
```
- Stop running the Minikube cluster:
```bash
minikube stop
```
- Delete the Minikube cluster:
```bash
minikube delete
```

#### Access Minikube Dashboard

- Run the command below to enable and access the Minikube dashboard:
```bash
minikube dashboard
```
- Alternatively, to access the dashboard directly via the browser, obtain the dashboard’s IP address:
```bash
minikube dashboard --url
```
