# Mini-projet-docker
This is a mini projet docker for bootcamp devops Eazytraining

Firstname : AUGET

Surname : Rabina

For Eazytraining's 19th DevOps Bootcamp

Period : May-June-July

Thursday the 09th, May 2024

LinkedIn : www.linkedin.com/in/auget-rabina-61663314a


# CONTEXT

The project aims to develop an adaptable and easily deployable microservices application, with the emphasis on maximum automation.

This POC (Proof of Concept) will illustrate the effectiveness of Docker and its usefulness in this context. Our aim is to create a Docker-based decoupling infrastructure 
for an existing application.

This process will facilitate and accelerate the deployment of new versions, while reducing adaptability problems.

So, I'm going to show you the contents of a very basic application that displays a list of students with their age.

# Application

The application is "student_list" and comprises two modules:

## the first module is a REST API (with basic authentication required) that sends the student's wish list based on a JSON file.
## The second module is a web application written in HTML + PHP that allows the end user to obtain a list of students.

And here are the application files:
student_age.py: contains the API source code in Python
student_age.json: contains the student's name and age in JSON format
Requirements.txt: contains all packages to be installed to run the application
You need to update the following line before running the website container so that api_ip_or_name and port match your deployment.
index.php: PHP page where the end user will be logged in to interact with the service to list students with their ages. 

# My role

Our task will be to create the following files according to the source files and instructions communicated by the development team:
Dockerfile: the file that will be used to build the API image
docker-compose.yml: to launch the application (API and Frontend)
docker-compose-registry.yml: to create a private registry where we'll store our docker images, and a web interface that will allow us to manage the registry from a browser.

# Infrastructure:

For this project, I will use the following technologies:
. Physical host: Windows 11
. Virtualbox 7.0
. Centos Stream 9
. Docker version 26.1.1 build 4cf5afa
. Docker Compose version v2.7.0
