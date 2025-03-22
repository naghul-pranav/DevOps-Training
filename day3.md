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

- Modify the port number from 3001 to 80 as follows:
```bash
EXPOSE 80
```
![git dockerfile after](https://github.com/user-attachments/assets/1b233a8b-5113-44ae-a753-8f2f59a5b85e)

- Then give 'Build now' in corresponding Jenkins pipeline:

![jenkins build 8 after edit dockefile](https://github.com/user-attachments/assets/e82c0333-7c48-49c5-a3b3-a602e949c3f0)

#### Create and navigate to 'docker' directory in Local Machine

- Create the repository 'docker'
```bash
mkdir docker
```
- Make 'docker' the current working directory
```bash
cd docker
```

#### Build Docker image inside the 'docker' directory

- Create a Dockerfile using the following command:
```bash
sudo nano Dockerfile
```
- In the Dockerfile, write the following content:
```groovy
# Use an official Node.js runtime as a base image
FROM node:18

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json ./
RUN npm install

# Copy the rest of the application
COPY . .

# Expose port 3000 and start the app
EXPOSE 3000
CMD ["npm", "start"]
```
![sudo nano dockerfile](https://github.com/user-attachments/assets/bdc89a9b-0e87-401c-b7fd-268d9c51504d)

- Install Node Package Manager (npm) in the terminal (Prerequisite step)
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

#### Navigate out of 'docker' directory

- Use the following command:
```bash
cd ..
```

#### Start the minikube cluster

- Create and start a local Kubernetes cluster (Prerequisite step)
```bash
minikube start
```
![1 minikube start](https://github.com/user-attachments/assets/b3973a13-0680-4148-8ced-0d1f08811475)

- Check the current status of the Minikube Kubernetes cluster (Optionalstep)
```bash
minikube status
```
![2 minikube status](https://github.com/user-attachments/assets/c05f908b-d253-4148-8852-aeb7d8c801a3)

#### Create and configue nginx-deployment.yaml file

- Create the nginx-deployment.yaml file
```bash
nano nginx-deployment.yaml
```
- Configure the nginx-deployement.yaml file
```groovy
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: naghuptanavkk/docker:latest 
        imagePullPolicy: IfNotPresent
        ports:
        - containerPort: 8080
```
![Screenshot from 2025-03-22 09-49-39](https://github.com/user-attachments/assets/bdbe3d79-b1d8-4451-b37d-77925aa65056)

#### Create and configue service.yaml file

- Create the nginx-deployment.yaml file
```bash
nano service.yaml
```
- Configure the nginx-deployement.yaml file
```groovy
apiVersion: v1
kind: Service
metadata:
  name: my-app
  namespace: default
spec:
  type: NodePort # Ensures external access via a specific port
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80 # Service port inside the cluster
      targetPort: 80 # The container's port
      nodePort: 30391 # Externally accessible port
```
![4 service yaml file](https://github.com/user-attachments/assets/aa39daa7-8151-4887-8edb-da039aa57997)

#### Create or update a Kubernetes resource and service resource

- Execute following command to create or update a Kubernetes resource
```bash
kubectl apply -f nginx-deployment.yaml
```
![5 kubectl apply nginx](https://github.com/user-attachments/assets/73f01202-a7a6-41eb-919a-79ead7866e9e)

- Execute following command to create or update a Kubernetes service resource
```bash
kubectl apply -f service.yaml
```
![6 kubectl apply service](https://github.com/user-attachments/assets/a435b477-e879-44c5-8be4-2bcb2bf086da)

#### List the nodes and pods in the Kubernetes cluster

- List all the nodes in the Kubernetes cluster
```bash
kubectl get nodes
```
![7 kubectl get nodes](https://github.com/user-attachments/assets/2e7a51ed-9661-45da-8d30-b78b880f7310)

- List all the pods in the Kubernetes cluster
```bash
kubectl get pods
```
![8 kubectl get pods](https://github.com/user-attachments/assets/da37e903-6b6e-4577-9b54-60fa1c212ea4)

#### Final stage of deploying Docker image

- Expose the minikube service in a browser
```bash
minikube service my-app
```
![9 minikube service my-app](https://github.com/user-attachments/assets/e67abe06-12d6-4379-afe7-ef3200c10ecb)

- The browser will display the project contained inside Docker image

![11 final output](https://github.com/user-attachments/assets/91b2ed62-1e0d-4407-8029-a7e333f0821a)

- Alternately we can run the following commands to open the minikube service in the browser
```bash
minikube service my-app --url
```
![10 minikube service my-app url](https://github.com/user-attachments/assets/78c8f6d1-d4f4-4656-a55c-64adf68458e8)

```bash
curl  http://192.168.49.2:30391
```

