# Installing and setting up Kubernetes Minikube

## Update system packages and Install dependencies
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget apt-transport-https conntrack socat
```
![image](https://github.com/user-attachments/assets/0019f77d-60d9-44fb-9cd9-030f88256d20)

## Install Docker, Kubectl and Minikube
### Install Docker
```bash
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
docker --version
```
### Install Kubectl
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version --client
```
### Install Minikube
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
```
![image](https://github.com/user-attachments/assets/f16981cd-567f-4641-bf39-caf64312b7ee)
![image](https://github.com/user-attachments/assets/f98aef39-c1a1-4941-8e16-fdeede4d2170)

### Fix Docker setup
```bash
sudo usermod -aG docker $USER
reboot
```

### Verify Installation after reboot
```bash
docker run hello-world
```
![image](https://github.com/user-attachments/assets/7f55cdfd-b47d-4fec-93c5-59bebbeee6fb)


## Start and open Minikube
```bash
minikube start --driver=docker
minikube dashboard
```
![image](https://github.com/user-attachments/assets/70a3995c-436e-472d-81ea-90920026d8e0)
![image](https://github.com/user-attachments/assets/8d49ff13-7975-4253-8983-37b241648eca)
