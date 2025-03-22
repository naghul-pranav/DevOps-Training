# Task 5

## Install Maven
```bash
sudo apt install maven
```

![install maven](https://github.com/user-attachments/assets/2196b0c0-b802-4f8a-a42f-c3cb08d5a88f)

## Fork the repo on github

![fork repo](https://github.com/user-attachments/assets/7b3b2b45-0c15-4b18-a16c-bb4d2397b600)

## Configure Jenkins
 - In Jenkins go to `configure jenkins` > `tools`
 - Locate JDK section
 - Uncheck `Install Automatically`
 - Name `Java 17`
 - Go to terminal and enter the command and get the java 17 path:

```bash
update-java-alternatives --list 
```

 - paste the java path in `JAVA_HOME`

![image](https://github.com/user-attachments/assets/e71ecf62-8ba8-4cf5-8cd5-1ef1e1cb694e)

 - 
