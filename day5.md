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

#### If maven version is less than 3.8.4, proceed with following steps:

- Remove Any Existing Maven Installation (If Any):
```bash
sudo apt remove --purge maven -y
```
- Download Maven 3.8.4
```bash
wget https://archive.apache.org/dist/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz
```
- Extract and Move Maven to /bin
```bash
wget https://archive.apache.org/dist/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz
```
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

 - paste the java path in `JAVA_HOME`

![image](https://github.com/user-attachments/assets/e71ecf62-8ba8-4cf5-8cd5-1ef1e1cb694e)

 - 
