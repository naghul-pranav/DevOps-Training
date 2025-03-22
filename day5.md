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

## Configure Jenkins
 - In Jenkins go to `Manage jenkins` > `tools`
 - Locate JDK section
 - Uncheck `Install Automatically`
 - Name `Java 17`
 - Go to terminal and enter the command and get the java 17 path:

```bash
update-java-alternatives --list 
```
![update java alternatives list](https://github.com/user-attachments/assets/36e84017-a3f9-4da3-be63-3a1a80ac81b7)

 - Paste the java path in `JAVA_HOME`

![image](https://github.com/user-attachments/assets/e71ecf62-8ba8-4cf5-8cd5-1ef1e1cb694e)

 - 
