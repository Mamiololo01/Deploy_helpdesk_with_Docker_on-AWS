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


Navigate back to your Instance Dashboard, select your newly created instance and click the “Connect” button.


Under the SSH client tab, locate the ssh command that will allow you to SSH into your instance via your local terminal. Copy the command.


Paste the command into your local terminal to login to your instance remotely.

Note: If you used a key pair to create your instance, your .pem key-pair file needs to be in the same directory of running this command. Otherwise, you will receive an “access denied” error.

Type “yes” when prompted to connect to the instance. And you will be logged into your cloud instance via your remote machine.


Step 2- Updating our Instance & Installing Docker
Now that we are logged in remotely, we need to update the packages on our machine by running sudo apt update:

sudo apt update

Next, we need to upgrade our local OS to reflect those updated changes by running sudo apt upgrade. You might be prompted to ‘reset’ your system by the CLI.

sudo apt upgrade

Now that our Ubuntu packages and systems have been downloaded and installed, we need to install docker and docker compose to be able to run containers on our instance. We start by running sudo apt install docker.io

sudo apt install docker.io

Next, we install docker-compose by running sudo apt install docker-compose -y.

sudo apt install docker-compose -y

Now that docker is installed, we can run docker ps to see if any containers are running.

Since we only just installed docker, there should be no containers listed.

sudo docker ps

Now our environment is ready for us to install our help desk.

Step 3: Installing and Configuring our Help Desk
Now we need to download our Help Desk and run it in a docker container. Today, I have chosen to build a Peppermint Help Desk.

Peppermint is a help desk solution similar to ServiceNow, Zendesk, or SysAid, or Zoho.

Peppermint has a great documentation on how to launch using Docker Containers. Here is a screen shot from the GitHub site. This template is slightly dated, but a good starting point. We are going to use this as our base ‘docker-compose.yml’ file for configuring our Peppermint help desk.


Starting in our home directory, we need to make a peppermint directory and navigate to it:

mkdir peppermint
cd peppermint

Now we need to make our docker-compose.yml file which will contain the configuration for installing our Peppermint Help Desk using docker containers.

nano docker-compose.yml
And paste the following YAML configuration into the file. I’ve updated it a bit from the Peppermint GitHub to reflect updated versions of Docker.


Now we only need to run one command to set up our first Peppermint Help Desk container

sudo docker-compose up -d
If this is your first time pulling down the docker image, it might take a first minutes.


Once completed, you should get a similar confirmation in your CLI:


Next, we run docker ps to retrieve the port # to test our new help desk in the browser.

sudo docker ps
We can see our Help Desk is running on port :5000, which we configured in our docker-compose.yml file.


If you were running this locally on your machine, you could type “localhost:5000” in your browser to check to see if your help desk is running.

Since we launched our via AWS EC2, we need to location our public DNS name and add our port number :5000 to check our results. We can locate this in the EC2 dashboard and paste that Public DNS name in our browser.


Wait! Why can’t reach our help desk?


Remember our Firewall settings? We forgot to allow ingress traffic from port :5000. Let’s revisit our security group settings and fix that now


Now let’s try visiting our public DNS name with the correct port number in our browser to see if our firewall fix changed our results:


With the updated firewall settings, we can now access the login of our Help Desk
Now, let’s login with our default username and password. The default email for peppermint is “admin@admin.com”. The default password is “1234”. You can change both once you login. (As you should).

Once logged in you can begin configuring your Help Desk as desired and share it with the world.


Congratulations! You just launched a peppermint help desk on a docker container using AWS!
