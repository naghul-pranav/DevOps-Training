# Task 5

## Install Maven

#### Install maven using the below command
```bash
sudo apt install maven
```

![install maven](https://github.com/user-attachments/assets/2196b0c0-b802-4f8a-a42f-c3cb08d5a88f)

#### Check whether maven is installed:
```bash
mvn -version
```
![1 version 1](https://github.com/user-attachments/assets/6b8e1908-9f56-4d25-bc57-65b5c8bc012e)

#### If maven version is less than 3.8.4, proceed with following steps:

- Remove Any Existing Maven Installation (If Any):
```bash
sudo apt remove --purge maven -y
```
![2 purge](https://github.com/user-attachments/assets/c90b1521-7e10-4b07-8780-7089130de095)

- Download Maven 3.8.4
```bash
wget https://archive.apache.org/dist/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz
```
![3 wget](https://github.com/user-attachments/assets/c8cc3863-4cac-477b-aff8-586408077bac)

- Extract and Move Maven to `/bin`
```bash
sudo tar -xvzf apache-maven-3.8.4-bin.tar.gz -C /usr/local
sudo ln -s /usr/local/apache-maven-3.8.4/bin/mvn /usr/bin/mvn
```
![4 sudo tar](https://github.com/user-attachments/assets/2407f31e-24b0-4d2a-8a5c-2a49def99857)

- Set Up Environment Variables
```bash
echo "export M2_HOME=/opt/maven" >> ~/.bashrc
echo "export PATH=\$M2_HOME/bin:\$PATH" >> ~/.bashrc
source ~/.bashrc
```
- Verify Maven Installation
```bash
mvn -version
```
![5 version](https://github.com/user-attachments/assets/866cf520-ad30-47c8-afee-14505d87a969)

## Fork the repo on github

![fork repo](https://github.com/user-attachments/assets/a7618436-3cd0-4ebe-93a4-99e679187fe1)

- Modify contents of `build.sh` and `deploy.sh` as follows
 `build.sh`
 ```groovy
 #!/bin/bash
 
 # Variables
 IMAGE_NAME="naghulpranavkk/mnv"
 TAG="latest"
 
 # Build Docker image
 docker build -t $IMAGE_NAME:$TAG .
 echo "Docker image $IMAGE_NAME:$TAG built successfully."
 ```
 `deploy.sh`
 ```groovy
 #!/bin/bash
 
 # Set Docker image name, tag, and container name
 IMAGE_NAME="naghulpranavkk/mnv"
 TAG="latest"
 CONTAINER_NAME="my_container"
 
 # Stop and remove any existing container with the same name
 docker stop $CONTAINER_NAME || true
 docker rm $CONTAINER_NAME || true
 
 # Run the new Docker container
 docker run -d -p 3002:80 --name $CONTAINER_NAME $IMAGE_NAME:$TAG
 ```

## Configure Jenkins

- In Jenkins go to `Manage jenkins` > `tools`

![manage jenkins](https://github.com/user-attachments/assets/514f7c23-f4db-402b-861a-d19b1ef2cf43)

- Locate JDK section

![jenkins tools 1](https://github.com/user-attachments/assets/b641430f-4f3d-4ac5-bcb9-3e9b5b4ae832)

- Name `Java 17`
- Go to terminal and enter the command and get the java 17 path:

```bash
update-java-alternatives --list 
```
![update java alternatives list](https://github.com/user-attachments/assets/36e84017-a3f9-4da3-be63-3a1a80ac81b7)

- Paste the java path in `JAVA_HOME`

![jenkins tools 2](https://github.com/user-attachments/assets/94617a19-2cb5-4fc9-a1e1-6ee99767367e)

- Uncheck `Install sutomatically` and click on `Save`

## Create new repository on docker named mvn

![docker mnv](https://github.com/user-attachments/assets/f3e6abcc-2b15-43eb-b4a9-037a4c9935e1)

## Create new pipeline on jenkins

- Go to `localhost:8080/`

![jenkins 1](https://github.com/user-attachments/assets/e118949e-c2dc-4db6-a1ef-1e4998de8272)

- Click on `New item`

![jenkins 2](https://github.com/user-attachments/assets/e937734c-0d8f-4e3a-a098-9ab9b4e282ae)

- Enter an item name and select Pipeline, then click `Ok`

![jenkins 3](https://github.com/user-attachments/assets/ae71d782-ea96-46c9-b0b0-79295f60b89a)

- In the Pipeline script, paste the following:
```groovy
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "naghulpranavkk/mnv"
        DOCKER_TAG = "latest"
        DOCKER_CREDENTIALS_ID = "docker-seccred"
        MAVEN_HOME = "/opt/maven"  // Updated Maven Path
        KUBECONFIG = "/var/lib/jenkins/.kube/config"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/naghul-pranav/MNV.git', branch: 'main'
            }
        }

        stage('Build Application') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS') {
                        sh '${MAVEN_HOME}/bin/mvn clean package -DskipTests'
                    }
                }
            }
        }

        stage('Run Maven Tests') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS') {
                        sh '${MAVEN_HOME}/bin/mvn test'
                    }
                }
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
                echo "Logging into Docker Hub..."
                withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS_ID, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo "Pushing Docker image to Docker Hub..."
                sh '''
                    docker tag $DOCKER_IMAGE:$DOCKER_TAG $DOCKER_IMAGE:$DOCKER_TAG
                    docker push $DOCKER_IMAGE:$DOCKER_TAG
                '''
            }
        }

        

        stage('Deploy Docker Container') {
            steps {
                echo "deploying..."
                sh 'chmod +x deploy.sh'
                sh './deploy.sh'
            }
        }
    }

    post {
        success {
            echo "✅ Deployment Successful!"
        }
        failure {
            echo "❌ Deployment Failed!"
        }
    }
}
```
- Then click on `Save`

## Build the Jenkins pipeline

- Now click on `Build Now`

- After build is successful, we can observe following pages in the jenkins webpage

![final 1](https://github.com/user-attachments/assets/2c692a61-ac1c-44a8-8198-5309e578df0b)

![final 2](https://github.com/user-attachments/assets/aa5c652d-125d-4916-a91b-05d462a6e210)

![final 3](https://github.com/user-attachments/assets/17305fe2-18ca-41ba-bdbb-a93e5747d4e4)


