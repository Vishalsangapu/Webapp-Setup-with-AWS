# Webapp-Setup-with-AWS
A CI/CD pipeline of a webapp in cloud 

VSCode

C:\Users\vsang\Downloads\devops> - (Keypair path downloaded from AWS console - to get the access to connect to EC2 instance)
cd ~/Downloads/devops ls
-a----        16-03-2025     13:54           1678 nextwork-keypair.pem - (Downloaded file)

to change permissions of the .pem file - (Windows version)

cd ~/Downloads/devops icacls "nextwork-keypair.pem" /reset
cd ~/Downloads/devops icacls "nextwork-keypair.pem" /grant:r "%vishal:R"
cd ~/Downloads/devops icacls "nextwork-keypair.pem" /inheritance:r

Connection to ec2 instance

cd ~/Downloads/devops ssh -i C:\Users\vsang\Downloads\devops\nextwork-keypair.pem ec2-user@ec2-98-81-255-161.compute-1.amazonaws.com
The authenticity of host 'ec2-98-81-255-161.compute-1.amazonaws.com (98.81.225.161)' can'
t be established.
ED25519 key is not known by any other names.
Are you sure you want to continue connecting (yes/no[fingerprint])? yes
cd ~/Downloads/devops ssh -i C:\Users\vsang\Downloads\devops\nextwork-keypair.pem ec2-user@ec2-98-81-255-161.compute-1.amazonaws.com

![Screenshot 2025-03-14 115624](https://github.com/user-attachments/assets/d98eefd5-51c1-4087-bf10-62b44588c153)

Here installing maven and amazon corretto 8 (java version) to bulild our web app

wget https://archive.apache.org/dist/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz

sudo tar -xzf apache-maven-3.5.2-bin.tar.gz -C /opt

echo "export PATH=/opt/apache-maven-3.5.2/bin:$PATH" >> ~/.bashrc

source ~/.bashrc

sudo dnf install -y java-1.8.0-amazon-corretto-devel

export JAVA_HOME=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64

export PATH=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64/jre/bin/:$PATH

Use mvn to generate a Java web app

mvn archetype:generate \
   -DgroupId=com.nextwork.app \
   -DartifactId=nextwork-web-project \
   -DarchetypeArtifactId=maven-archetype-webapp \
   -DinteractiveMode=false

![Screenshot 2025-03-17 112817](https://github.com/user-attachments/assets/84ab916e-964f-40ad-afaa-4647326e3046)


Connect VSCode with EC2 Instance
installing Vscode remote SSh connection extension

![Screenshot 2025-03-17 113008](https://github.com/user-attachments/assets/3196425d-4dbe-43d5-a1ca-ee11b5e72fc9)

![Screenshot 2025-03-17 113043](https://github.com/user-attachments/assets/72717957-eafb-4e5f-9437-d4922cbdb2bb) to config out ex2 host connection

Enter the SSH command you used to connect to your EC2 instance: ssh -i [PATH TO YOUR .PEM FILE] ec2-user@[YOUR PUBLIC IPV4 DNS]
![Screenshot 2025-03-17 113135](https://github.com/user-attachments/assets/6b90d02c-2993-4b90-b6da-40d14a1bb4ae) - Adding our host info 

Connected to ec2 instance

Select Open folder.
At the top of your VSCode window, you should see a drop down of different file and folder names.
Enter /home/ec2-user/nextwork-web-project.
![Screenshot 2025-03-17 113926](https://github.com/user-attachments/assets/771d3828-e590-4a5d-ae96-c72179e8010d)

by acceptiong a trust code pop, this will enable the web files required to run an application

![Screenshot 2025-03-17 114009](https://github.com/user-attachments/assets/e415cd52-b9ce-4926-84db-a383f907f459)

expanding all the subfolders, provides us the artifactry mvn and java files in there repository
![Screenshot 2025-03-17 114126](https://github.com/user-attachments/assets/e423108b-d00b-47b7-a582-93ae7bf9bf7d)

exploring index file
<html>
<body>
<h2>Hello {YOUR NAME}!</h2>
<p>This is my NextWork web application working!</p>
</body>
</html>

save the changes hence we're done with bulding our web app
