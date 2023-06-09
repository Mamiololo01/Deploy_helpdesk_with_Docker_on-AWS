# Deploy_helpdesk_with_Docker_on-AWS
Implementing Help Desk application with Docker Containers on AWS Services

How to Build an agile Help Desk using Docker Containers on AWS Services


Introduction
In today’s fast-paced digital landscape, businesses need robust and efficient solutions to handle customer support and technical assistance. One such solution that combines the power of containerization and cloud computing is the creation of a Help Desk using Docker containers on AWS services.

In this tech-walkthrough, we will embark on a journey to build a scalable and flexible Help Desk infrastructure that will revolutionize your customer support operations.

Let’s get building!

Pre-Requisites
Basic understanding of Docker and containerization concepts.
Familiarity with AWS services such as Amazon ECS, IAM, VPC, RDS, and CloudWatch.
Access to an AWS account with sufficient permissions to create and manage resources.
Prior knowledge of networking principles and configuring security groups in AWS.
Proficiency in using the command line interface (CLI) for Docker and AWS.

Step 1 — Setting up our Instance
Login to your AWS account and navigate to the EC2 instance dashboard. Click “Launch Instance”.


Give your instance a name. Select an OS and other settings as needed. Finally click “Launch Instance”.

<img width="1037" alt="Screenshot 2023-05-16 at 08 02 16" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/c126542c-8b2a-4671-981f-3d2004e2c864">

<img width="943" alt="Screenshot 2023-05-16 at 08 02 29" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/6a5622be-d77e-4d2e-9dd4-37004229f204">



Once launched you will receive a confirmation.

<img width="1066" alt="Screenshot 2023-05-16 at 08 02 36" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/5b891cc9-581e-4d3b-a32b-4601bd5e7969">

<img width="1176" alt="Screenshot 2023-05-16 at 08 06 30" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/e9c942c2-44b3-49e0-bfa3-30ba2062c381">

<img width="1030" alt="Screenshot 2023-05-16 at 08 07 05" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/f6ebd80b-5ccc-49ee-afb0-a28f8b7947ba">


Navigate back to your Instance Dashboard, select your newly created instance and click the “Connect” button.


Under the SSH client tab, locate the ssh command that will allow you to SSH into your instance via your local terminal. Copy the command.


Paste the command into your local terminal to login to your instance remotely.

Note: If you used a key pair to create your instance, your .pem key-pair file needs to be in the same directory of running this command. Otherwise, you will receive an “access denied” error.

Type “yes” when prompted to connect to the instance. And you will be logged into your cloud instance via your remote machine.


Step 2- Updating our Instance & Installing Docker
Now that we are logged in remotely, we need to update the packages on our machine by running sudo apt update:

sudo apt update

<img width="722" alt="Screenshot 2023-05-16 at 08 34 31" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/f3bdcb60-bc09-479a-9dea-e7f9f789a892">

Next, we need to upgrade our local OS to reflect those updated changes by running sudo apt upgrade. You might be prompted to ‘reset’ your system by the CLI.

sudo apt upgrade


<img width="666" alt="Screenshot 2023-05-16 at 08 35 10" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/74a2b372-68fe-4974-be51-996a9ab7cff2">

Now that our Ubuntu packages and systems have been downloaded and installed, we need to install docker and docker compose to be able to run containers on our instance. We start by running sudo apt install docker.io

sudo apt install docker.io

<img width="701" alt="Screenshot 2023-05-16 at 08 38 00" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/8cf01d7f-c851-49ac-af59-375cd8192a84">

Next, we install docker-compose by running sudo apt install docker-compose -y.

sudo apt install docker-compose -y

<img width="707" alt="Screenshot 2023-05-16 at 08 38 40" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/ff8b8c6e-db45-490f-875b-42b7c50c114f">

Now that docker is installed, we can run docker ps to see if any containers are running.

Since we only just installed docker, there should be no containers listed.

sudo docker ps


<img width="711" alt="Screenshot 2023-05-16 at 08 39 12" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/1428b83e-8f5d-4323-9841-823003a0d9c8">

Now our environment is ready for us to install our help desk.

Step 3: Installing and Configuring our Help Desk
Now we need to download our Help Desk and run it in a docker container. Today, I have chosen to build a Peppermint Help Desk.

Peppermint is a help desk solution similar to ServiceNow, Zendesk, or SysAid, or Zoho.

Peppermint has a great documentation on how to launch using Docker Containers. Here is a screen shot from the GitHub site. This template is slightly dated, but a good starting point. We are going to use this as our base ‘docker-compose.yml’ file for configuring our Peppermint help desk.


Starting in our home directory, we need to make a peppermint directory and navigate to it:

mkdir peppermint
cd peppermint

<img width="555" alt="Screenshot 2023-05-16 at 08 41 32" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/458d3c40-7280-426d-8be6-4216df304eda">

Now we need to make our docker-compose.yml file which will contain the configuration for installing our Peppermint Help Desk using docker containers.

nano docker-compose.yml
And paste the following YAML configuration into the file. I’ve updated it a bit from the Peppermint GitHub to reflect updated versions of Docker.

<img width="661" alt="Screenshot 2023-05-16 at 08 42 11" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/7f927989-6862-495e-a43e-350d2df4095b">

Now we only need to run one command to set up our first Peppermint Help Desk container

sudo docker-compose up -d
If this is your first time pulling down the docker image, it might take a first minutes.

<img width="732" alt="Screenshot 2023-05-16 at 08 46 53" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/3832454d-5f04-40e0-9a97-f97ff36414ce">

<img width="727" alt="Screenshot 2023-05-16 at 08 47 46" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/2cda4c3a-285a-4f87-84f5-706e0265f712">

Once completed, you should get a similar confirmation in your CLI:


Next, we run docker ps to retrieve the port # to test our new help desk in the browser.

sudo docker ps
We can see our Help Desk is running on port :5000, which we configured in our docker-compose.yml file.

<img width="716" alt="Screenshot 2023-05-16 at 09 07 52" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/1b72ca71-b20b-4e96-8ebe-c1bb1cbc1952">

If you were running this locally on your machine, you could type “localhost:5000” in your browser to check to see if your help desk is running.

Since we launched our via AWS EC2, we need to location our public DNS name and add our port number :5000 to check our results. We can locate this in the EC2 dashboard and paste that Public DNS name in our browser.


Wait! Why can’t reach our help desk?


Remember our Firewall settings? We forgot to allow ingress traffic from port :5000. Let’s revisit our security group settings and fix that now


Now let’s try visiting our public DNS name with the correct port number in our browser to see if our firewall fix changed our results:


With the updated firewall settings, we can now access the login of our Help Desk
Now, let’s login with our default username and password. The default email for peppermint is “admin@admin.com”. The default password is “1234”. You can change both once you login. (As you should).

Once logged in you can begin configuring your Help Desk as desired and share it with the world.


Congratulations! You just launched a peppermint help desk on a docker container using AWS!


<img width="1257" alt="Screenshot 2023-05-16 at 09 08 19" src="https://github.com/Mamiololo01/Deploy_helpdesk_with_Docker_on-AWS/assets/67044030/1438ac23-57b2-4b7d-96c5-70e7ee394541">
