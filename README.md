# Mini-projet-docker
This is a mini projet docker for bootcamp devops Eazytraining

Firstname : AUGET

Surname : Rabina

For Eazytraining's 19th DevOps Bootcamp

Period : May-June-July-2024

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

+ the first module is a REST API (with basic authentication required) that sends the student's wish list based on a JSON file.
+ The second module is a web application written in HTML + PHP that allows the end user to obtain a list of students.

And here are the application files:

+ student_age.py: contains the API source code in Python
+ student_age.json: contains the student's name and age in JSON format
+ Requirements.txt: contains all packages to be installed to run the application
+ index.php: PHP page where the end user will be logged in to interact with the service to list students with their ages. 

# My role

Our task will be to create the following files according to the source files and instructions communicated by the development team:

+ Dockerfile: the file that will be used to build the API image
+ docker-compose.yml: to launch the application (API and Frontend)
+ docker-compose-registry.yml: to create a private registry where we'll store our docker images, and a web interface that will allow us to manage the registry from a browser.

# Infrastructure:

For this project, I will use the following technologies:

+ Physical host: Windows 11
+ Virtualbox 7.0
+ Centos Stream 9
+ Docker version 26.1.1 build 4cf5afa
+ Docker Compose version v2.7.0

# Build step

1. We'll create a "mini-project" folder, move around inside it and create the Dokerfile using the commands below 

   + mkdir mini-projet
   + cd mini-projet
   + git clone the repository
   + cd student_list/simple_api
   + nano Dockerfile (To describe the steps involved in creating a docker image)

2. Once we have created the dockerfile, bwe have to build the image:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/ec46802b-bdf7-4067-b8ff-15491cc001bd)

3.Let's check that the image has been created correctly:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/b7bd6d36-1f4c-4092-be8d-f37061e72dd5)

4. We're now going to start the docker container from the image we've just created on port 5000:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/8e3862e9-a3bb-416c-9ecb-deef969e7ee6)

5. Let's check that the container has been launched:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/01baf04d-b0b5-4458-ac90-7f900b11c038)

6. Now, let's confirm that the API is working.We can make a request to the container from the physical host, specifying the user name and password supplied by the development team.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/c5a0f123-ff20-4063-83e2-5e4ac04975a5)

7. We can now move on to creating the docker compose file to deploy the API and Frontend. To start afresh, we'll delete the container we've created.

Note that we can remove containers or images easily by indicating only the first three characters of the ID.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/245aece5-8cbc-471f-ad5c-c1068d50180e)

Unfortunately here, I have two different tags of the image, that's why it displays that the image is untagged. I can't delete it outright because I'm on a limited connection.
And I can't completely delete the image in question because it's still going to be useful for the rest of the project.

# Infrastructure As Code

1. After deleting the container and image, we created the docker-compose.yml file (you'll find it in the repository), which we'll use to deploy/manage/bind together the frontend in an API-dependent way.
Let's launch it:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/ab912220-a272-42f7-a9be-77960402ff63)

Here we can see that the API and Frontend containers have been created, as well as the mini-project_pozos_network we declared in the docker-compose file.
The -d option is used to launch containers in the background.

2. Let's check that the containers have been launched using the "docker ps" command:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/ff8ab2fb-a1f1-4d64-812a-95e9d998b63a)

We can see that containers are running and the frontend is listening on port 80.

3. We can now run a test via a browser. Note that a modification has also been made to the index.php file so that its IP points to the name of the API container in the docker-compose.
So, whatever the IP of the container, the API will always be accessible.

![image](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/45d352e3-1ea5-4aa4-924b-74a3d35d69a9)

4. The application works correctly. You may have noticed that my container is listening on port 80 while my browser is making a request on port 8081.
This is because I'm using virtualbox to virtualize my docker host, so I have to use NAT to access it from my physical host.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/6aff7b16-5fb0-4479-b3cc-3623b473390d)

5. Since my docker is in a virtual machine on virtualbox, I have to do a NAT before I can view the website from my physical host.

Go to virtual machine configuration > Network > Advanced > Port forwarding:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/e619ecfe-1b9c-4d5f-823b-8b050b8232ee)

This will allow us to access the containerised application website from our physical host.

![image](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/4760b7ef-0f0e-4cea-94b8-4dcccc4cefb2)

The application is working properly.

# Private registry docker

1. The docker-compose-registry.yml file has now been created. As before, we'll launch the registry and user interface containers with the "docker-compose up -d" command.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/ba5e23fe-7878-43cb-8a30-5d1f86083d0b)

2. Let's check that the containers have been launched:

![docker ps private](https://github.com/rabinauget/mini-projet-docker/assets/61904489/92e9a395-4925-4346-be60-55ea987672bd)

3. Let's check from a browser that the UI is accessible:

But first, we need to add port forwarding in the virtual machine configuration to access the containerised UI from our physical host. To do this, go to virtual machine configuration > Network > Port forwarding:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/f3e7ebe9-b306-452a-9fd4-b733d38bb328)

The registry and the UI are working properly.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/b1bf3ad6-df84-4c48-82ea-163e91ce1bd5)

4. We can now push our images into the registry. First, we need to consult the list of images with the "docker images" command to find out which image we're going to push so that we can tag it.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/ebcdf2aa-ff7c-4dde-a25c-a4cc8ac01f74)

5. Then tag the images like this:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/e3a8c1d4-f8b4-44c7-95c4-0f7c0c89a259)

6. Let's check that the images have been tagged:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/0e479deb-9a51-4cbe-8a0f-41cb88d3a634)

We can see that image names are now prefixed with "localhost:5000".

7. We can now push images via docker push like this. We can see here that I already have some of the image's layers in the register, as I'd already done some testing.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/34426492-982c-4b7f-851d-59f636efe06e)

And we push all the images we've just tagged in the same way.

8. Now we can see from the browser that the images have been pushed.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/a5a71b29-f62f-48f7-b13d-81144408242b)

For example, you can click on a docker image and get all the details about that image.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/39dad0b7-7595-442c-b215-55edd20ba54f)

Then click on History for a more detailed view of the image. Then click on History to get a more detailed view of the image, and it's even possible to see the contents of the Dockerfile used to create the image.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/31dcbf98-fc6d-4639-b9ab-c7d6a4465023)

# Conclusion

This project gave me a better understanding of microservice infrastructure, and deepened my technical knowledge of docker.
Configuring the Dockerfile, docker-compose.yml, images, volumes and networks, as well as the various diagnostic commands, enabled me to discover all the layers that make up Docker. 
I'm now in a better position to contribute to the improvement of containerization processes within my team.















