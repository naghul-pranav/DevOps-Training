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

- Extract and Move Maven to /bin
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

- Modify contents of build.sh and deploy.sh as follows
 - build.sh
 ```groovy
 #!/bin/bash
 
 # Variables
 IMAGE_NAME="naghulpranavkk/mnv"
 TAG="latest"
 
 # Build Docker image
 docker build -t $IMAGE_NAME:$TAG .
 echo "Docker image $IMAGE_NAME:$TAG built successfully."
 ```
 - deploy.sh
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
 - Uncheck `Install Automatically`
 ![jenkins tools 1](https://github.com/user-attachments/assets/b641430f-4f3d-4ac5-bcb9-3e9b5b4ae832)

 - Name `Java 17`
 - Go to terminal and enter the command and get the java 17 path:

```bash
update-java-alternatives --list 
```
![update java alternatives list](https://github.com/user-attachments/assets/36e84017-a3f9-4da3-be63-3a1a80ac81b7)

 - Paste the java path in `JAVA_HOME`

![jenkins tools 2](https://github.com/user-attachments/assets/94617a19-2cb5-4fc9-a1e1-6ee99767367e)

 - 
