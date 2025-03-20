<h1 style="font-size: 100px;">Creating a Docker image using Jenkins</h1>

# Setting up Docker

## Step 1: Update the package list

  - First, ensure your package list is up to date:

```bash
sudo apt update
```
![1](https://github.com/user-attachments/assets/9cfb6e56-77db-4fc1-a90f-041cc51fa946)

## Step 2: Install dependencies

  - Install the required dependencies:

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
![2](https://github.com/user-attachments/assets/1e88fe1b-14b1-4a48-9c11-83aa80e0fdd8)

## Step 3: Add Docker's official GPG key

  - Next, add Docker’s official GPG key to ensure the software you’re installing is verified:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
![3](https://github.com/user-attachments/assets/bc0cc965-1563-45d6-8334-158452f5393c)

## Step 4: Add the Docker repository

  - Add Docker’s official repository to your system:
```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
![4](https://github.com/user-attachments/assets/f52efde7-03a8-4bf8-a087-d38878a9f72c)

## Step 5: Update the package list again

  - After adding the Docker repository, update the package list again:
```bash
sudo apt update
```
![5](https://github.com/user-attachments/assets/c246d475-af5f-407c-b7d1-641b66ce3e2b)

## Step 6: Install Docker

  - Now, install Docker:
```bash
sudo apt install docker-ce
```
![6](https://github.com/user-attachments/assets/1d51e9fe-55e5-410a-9e80-a1eb4c7fb1f7)
![7](https://github.com/user-attachments/assets/e591071f-383c-453b-8498-2b30207f9b63)

## Step 7: Verify Docker installation

  - To verify that Docker has been installed correctly, check its version:
```bash
docker --version
```
![8](https://github.com/user-attachments/assets/22199784-2fee-415a-bba3-9c130077fb6a)

  - You should see Docker's version information if it's installed correctly.

## Step 8: Run Docker without sudo (Optional)

  - If you want to run Docker commands without needing to prepend sudo, you can add your user to the docker group:
```bash
sudo usermod -aG docker $USER
```
![9](https://github.com/user-attachments/assets/4d4dea52-40e9-4faf-a736-f4875670d451)

  - You’ll need to log out and back in, or run:
```bash
newgrp docker
```
![10](https://github.com/user-attachments/assets/244e8032-5606-45f4-88d9-f608892336ab)

## Step 9: Start and enable Docker (Optional)

  - If Docker isn't automatically started, you can start and enable it to run on system boot:
```bash
sudo systemctl start docker
sudo systemctl enable docker
```
![11](https://github.com/user-attachments/assets/9e3c5ca7-cd63-4924-8e21-aed5ea0a461b)

That’s it! Docker should now be installed and running on your Ubuntu system.

## Installing Docker
  - Enter the following commands to inatall and verify installation of Docker
```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker --now
docker
```
![image](https://github.com/user-attachments/assets/e0a899be-cb40-40cf-9231-e35ce45a6e4f)
![image](https://github.com/user-attachments/assets/cbfdbef3-ad47-488b-89f5-0b450c27e3af)

## Download Docker plugins in Jenkins
 - Go to Jenkins `Dashboard` -> `Manage Jenkins` -> `Available Plugins` -> Search `Docker`
 - Select these plugins and Install
    - Docker
    - Docker Commons
    - Docker Pipeline
    - docker-build-step
    - CoudBees Docker Build and Publish

![image](https://github.com/user-attachments/assets/5eef535f-2b65-44ca-9ac2-2a19548477c5)
![image](https://github.com/user-attachments/assets/3f4bda54-a3dc-4811-a546-b027d83a679f)
![image](https://github.com/user-attachments/assets/f27a51c0-f7d0-4ea2-808e-161a16d296d4)

 - In this page Check the `Restart Jenkins` after installation this will restart Jenkins

![image](https://github.com/user-attachments/assets/023e655e-e8e7-4b3b-9b74-317f9f4484f2)

## Add Jenkins to Docker group
 - Go to terminal and run these commands to add Jenkins to docker group
```bash
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
sudo reboot
```
- This will do its thing and reboot the system 

## Setting up docker credentials
 - Go to Jenkins > `Manage Jenkins` > `Credentials` > `System` > `Global Credentials (Unrestricted)` > `Add Credentials`
 -  Fill your Docker hub `username` , `password`, and in the `id` field enter `docker-seccred`

![image](https://github.com/user-attachments/assets/c9e87ffe-6776-48ae-ab68-440eb5310626)

## Creating and building a pipeline

 - Go to Jenkins `Dashboard` > `Create a Job`

![image](https://github.com/user-attachments/assets/cd3138ce-07b3-4070-97b9-0a8d76df4a36)

 - Enter a project name 
 - Select `pipeline`
 - Click `Ok`

![image](https://github.com/user-attachments/assets/3b2b76ed-f099-4257-8669-cf269e4d10a3)

 - Go to `pipeline`
 - Paste this script below and change the credential wherever mentioned:
```groovy
pipeline {
    agent any

    environment {
        IMAGE_NAME = "sanjai4334/docker"          // Replace with your Docker Hub username and image name
        TAG = "latest"
        CONTAINER_NAME = "my-container"
        PORT = "3001"
    }

    stages {
        
        stage('Clone Repository') {
            steps {
                echo "Cloning GitHub repository..."
                git 'https://github.com/sanjai4334/docker.git'  // Replace with your repo URL
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh 'chmod +x build.sh'
                sh './build.sh'
            }
        }

                stage('Login to Docker Hub') {
            steps {
                echo "Logging into Docker Hub..." // Change the cedentialsID if you have docker credentials already added with another id other than docker-seccred
                withCredentials([usernamePassword(credentialsId: 'docker-seccred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo "Pushing Docker image to Docker Hub..."
                sh "docker tag $IMAGE_NAME:$TAG $IMAGE_NAME:$TAG"
                sh "docker push $IMAGE_NAME:$TAG"
            }
        }

        stage('Deploy Docker Container') {
            steps {
                echo "Deploying Docker container..."
                sh 'chmod +x deploy.sh'
                sh './deploy.sh'
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
        }
        failure {
            echo "Deployment Failed!"
        }
    }
}
```
 - click `save`
 - click `build`

![image](https://github.com/user-attachments/assets/7fad77f3-d083-414c-86fb-5ec0145a4b6d)

 - Go to Docker Hub to see your image pushed there

![image](https://github.com/user-attachments/assets/e07c5427-63f9-4b5e-b4c9-091cdb8cf5c1)

