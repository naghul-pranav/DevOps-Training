# Installing Jenkins in Linux and creating a freestyle nginx project

## Installing JDK 17

#### Update the package list

  - First, ensure your package list is up to date:

```bash
sudo apt update
```
![1 sudo apt update](https://github.com/user-attachments/assets/1daaa9a1-842c-49a4-a2be-75b28bb69082)

#### Check if you already have Java in your device
```bash
java -version
```
![2 java --version](https://github.com/user-attachments/assets/f8f1025b-9ff0-457a-8c47-14547bbc4d26)

#### If not installed, execute the following command
```bash
sudo apt install opensdk-17-sdk -y
```
![3 sudo apt install openjdk-17-jdk -y](https://github.com/user-attachments/assets/81180b19-b048-4dd6-894b-11b12ff9be7b)

## Installing Jenkins

#### Execute the following commands in your terminal

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
```
![4 sudo wget O](https://github.com/user-attachments/assets/71a1f29e-cf12-4851-90b4-fd33015335ea)

```bash
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```
![5 echo deb](https://github.com/user-attachments/assets/2fb7d860-dd13-4e76-803f-5cd910d38010)

```bash
sudo apt-get update
```
![6 sudo get-apt update](https://github.com/user-attachments/assets/a9acc0aa-0c98-459d-a9f3-af1965284e1e)

```bash
sudo apt-get install jenkins
```
![7 sudo install jenkins](https://github.com/user-attachments/assets/19b473d7-5688-48be-9569-9a0bcaaa7af1)

## Jenkins Initial Setup

- Open a browser and go to `localhost:8080` and we will see the below page

![8 unlock jenkins](https://github.com/user-attachments/assets/d7deb17a-33d1-48ff-97e4-cc3db3a317a8)

- Now go back to terminal and execute the below command to get admin password
```bash
sudo more /var/lib/jenkins/secrets/initialAdminPassword
```
![9 sudo more admin pass](https://github.com/user-attachments/assets/e2991ff0-71ad-4943-9fc7-287177a53156)

- Now again come back to browser and fill the admin password

![10 unlock jenkins](https://github.com/user-attachments/assets/52f3dcbb-0ce6-4426-95dd-bac2c3d1721d)

- Click on `continue`

![11 customize jenkins](https://github.com/user-attachments/assets/2e15ce02-6d67-453e-9723-160ad15456ce)

- Click on `Install Suggested Plugins`

![12 getting started](https://github.com/user-attachments/assets/dcc3b613-59a3-45bd-8236-7066940901df)

- The plugins will be installed one by one and you'll be redirected to the next page click `Start Jenkins`

- Fill in your details and create user id and password then click `save and continue`
> [!NOTE]  
> Remember this user id and password. This will overwrite the `Initial Password` generated, and will be required to login everytime you restart Jenkins.

![1](https://github.com/user-attachments/assets/7dc3ae3c-85f4-4820-80a4-9b455affc3ae)

- Leave the default Jenkins URL then click `Save and Finish`

## Setting up a Nginx freestyle project in Jenkins
 - In Jenkins home page click on `create a job`

![1](https://github.com/user-attachments/assets/90d7c7fb-50ed-4bd3-93f4-5afb45a29734)

 - Enter a project name
 - Select `Freestyle Project`
 - Click `Ok`

![1](https://github.com/user-attachments/assets/03d4672d-21e5-467f-9742-035c662784b8)

 - In the next page scroll down to `Build Steps`
 - Click `Add Build Step`
 - Select `Execute Shell`

![1](https://github.com/user-attachments/assets/60f7d6b0-85e9-44eb-a78b-9a94e8d46a94)

 - Paste in the below code
```bash
#!/bin/bash
# Update package lists
sudo apt update -y

# Install Nginx
sudo apt install -y nginx

# Start and enable Nginx
sudo systemctl enable nginx.service
sudo systemctl start nginx

# Verify Nginx is running
systemctl status nginx
```

![1](https://github.com/user-attachments/assets/27fd056c-ea7e-4069-9f23-fd7887260f96)

 - Click `Build Now` in the left side panel
   
![1](https://github.com/user-attachments/assets/290bb3be-cf50-40e8-b42e-a1cc9e2f2341)

 - Your first Nginx project using Jenkins is successfully deployed!
 - Click on the Build in `Builds` and click on the `Console Output` to view the logs
![1](https://github.com/user-attachments/assets/7a1271e1-da3a-4a32-95f0-de143585f826)
