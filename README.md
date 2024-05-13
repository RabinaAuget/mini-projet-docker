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
   + touch Dockerfile

2. Creating the Dockerfile with the command: touch Dockerfile

3. Build the image from Dockerfile

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/ec46802b-bdf7-4067-b8ff-15491cc001bd)

4.Let's check that the image has been created correctly:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/b7bd6d36-1f4c-4092-be8d-f37061e72dd5)

5. We're now going to start the docker container from the image we've just created on port 5000:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/8e3862e9-a3bb-416c-9ecb-deef969e7ee6)

6. Let's check that the container has been launched:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/01baf04d-b0b5-4458-ac90-7f900b11c038)

7. Now, let's confirm that the API is working.We can make a request to the container from the physical host, specifying the user name and password supplied by the development team.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/c5a0f123-ff20-4063-83e2-5e4ac04975a5)

8. We can now move on to creating the docker compose file to deploy the API and Frontend. To start afresh, we'll delete the container we've created.

Note that we can remove containers or images easily by indicating only the first three characters of the ID.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/245aece5-8cbc-471f-ad5c-c1068d50180e)

Unfortunately here, I have two different tags of the image, that's why it displays that the image is untagged. I can't delete it outright because I'm on a limited connection.
And I can't completely delete the image in question because it's still going to be useful for the rest of the project.

# Infrastructure As Code

1. After deleting the container and image, we created the docker-compose.yml file (you'll find it in the repository), which we'll use to deploy/manage/bind together the frontend in an API-dependent way.
Let's launch it:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/befb5c1d-4dde-4f50-9dae-23fe648a5c72)

Here we can see that the API and Frontend containers have been created, as well as the mini-project_pozos_network we declared in the docker-compose file.
The -d option is used to launch containers in the background.

2. Let's check that the containers have been launched using the "docker ps" command:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/edaae54e-7963-4041-beed-f4d76ab5d657)

We can see that containers are running and the frontend is listening on port 80.

3. We can now run a test via a browser. Note that a modification has also been made to the index.php file so that its IP points to the name of the API container in the docker-compose.
So, whatever the IP of the container, the API will always be accessible.

![image](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/45d352e3-1ea5-4aa4-924b-74a3d35d69a9)

4. The application works correctly. You may have noticed that my container is listening on port 80 while my browser is making a request on port 8081.
This is because I'm using virtualbox to virtualize my docker host, so I have to use NAT to access it from my physical host.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/7b2fbe23-810d-4e38-983f-030ed50a41cc)

5. Since my docker is in a virtual machine on virtualbox, I have to do a NAT before I can view the website from my physical host.

Go to virtual machine configuration > Network > Advanced > Port forwarding:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/e619ecfe-1b9c-4d5f-823b-8b050b8232ee)

This will allow us to access the containerised application website from our physical host.

![image](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/4760b7ef-0f0e-4cea-94b8-4dcccc4cefb2)

The application is working properly.

# Private registry docker

1. The docker-compose-registry.yml file has now been created. As before, we'll launch the registry and user interface containers with the "docker-compose up -d" command.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/953d7474-398d-45e0-bf5d-dddfd5f65d1f)

2. Let's check that the containers have been launched:

![compose](https://github.com/rabinauget/mini-projet-docker/assets/61904489/9ef86ffe-8b18-48fc-802e-0fc5fe75444e)

3. We can also see with "docker log" to confirm that the UI has been launched:

![log](https://github.com/rabinauget/mini-projet-docker/assets/61904489/3770dbb3-7120-4160-bc96-3d4a4d3391e5)

4. Let's check from a browser that the UI is accessible:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/505477b9-f1b4-4821-ba78-b161228248e6)

5. We can now push our images into the registry. First, we need to consult the list of images with the "docker images" command to find out which image we're going to push so that we can tag it.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/9c9076fd-ddff-4c7b-985c-a45468bfb2ba)

6. Then tag the images like this:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/cd2ad82e-2bf5-47d7-b6af-c90e552122e0)

7. Let's check that the images have been tagged:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/40054681-f901-4441-b643-8eed005772fd)

We can see that image names are now prefixed with "localhost:5000".

8. We can now push images via docker push like this. We can see here that I already have some of the image's layers in the register, as I'd already done some testing.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/83c98b16-c7f1-4441-8ca6-d0d9238ffef2)

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/c29bd6d2-79a0-4f6b-ae0b-8e2bd24ce2bf)

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/a4e50726-fedf-41bd-bc22-c66f25ccdf02)

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/be4077c0-a564-4e8b-afb7-16c4f3c650c4)

9. Now we can see from the browser that the images have been pushed.

But first, we need to add port forwarding in the virtual machine configuration to access the containerised UI from our physical host. To do this, go to virtual machine configuration > Network > Port forwarding:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/f3e7ebe9-b306-452a-9fd4-b733d38bb328)

The registry and the UI are working properly.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/8777f093-8d72-47fc-b600-aa084e9aa245)

# Conclusion

This project gave me a better understanding of microservice infrastructure, and deepened my technical knowledge of docker.
Configuring the Dockerfile, docker-compose.yml, images, volumes and networks, as well as the various diagnostic commands, enabled me to discover all the layers that make up Docker. 
I'm now in a better position to contribute to the improvement of containerization processes within my team.















