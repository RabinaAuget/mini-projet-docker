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

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/96514830-28b1-4178-9a24-8ac30042d309)

4. We're now going to start the docker container from the image we've just created on port 5000:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/1ef7f21c-d910-41a0-bfbf-cfdae7f9bd9d)

5. Let's check that the container has been launched:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/57c8ea6a-7f18-4deb-ad22-bdc637d4dd51)

6. Now, let's confirm that the API is working. But first, we need to change the IP of the url on line 29 of website/index.php so that it points to to localhost.
   Otherwise, our request will return an error.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/3110ce43-2af4-4810-878c-437f42cb4c63)

7. We can make a request to the container from the physical host, specifying the user name and password supplied by the development team.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/b0cb07c6-9e06-4177-b49f-6d8bd91fb64d)

8. We can now move on to creating the docker compose file to deploy the API and Frontend. To start afresh, we'll delete the container we've created.

Note that we can remove containers or images easily by indicating only the first three characters of the ID.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/181e2536-c46f-4cf6-9e9e-49fb93c966f5)

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/d55393d5-b6f7-400f-9849-8e24f17b7778)

Unfortunately here, I have two different tags of the image, that's why it displays that the image is untagged. I can't delete it outright because I'm on a limited connection.
And I can't completely delete the image in question because it's still going to be useful for the rest of the project.

# Infrastructure As Code

1. After deleting the container and image, we created the docker-compose.yml file (you'll find it in the repository), which we'll use to deploy/manage/bind together the frontend in an API-dependent way.
Let's launch it:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/13722b3f-1caa-431e-8749-3f97ef759311)

Here we can see that the API and Frontend containers have been created, as well as the mini-project_pozos_network we declared in the docker-compose file.
The -d option is used to launch containers in the background.

2. Let's check that the containers have been launched using the "docker ps" command:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/a224f559-c95d-4c7b-aafe-761523e44d40)

We can see that containers are running and the frontend is listening on port 80.

3. We can now run a test via a browser. Note that a modification has also been made to the index.php file so that its IP points to the name of the API container in the docker-compose.
So, whatever the IP of the container, the API will always be accessible.

![image](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/45d352e3-1ea5-4aa4-924b-74a3d35d69a9)

4. The application works correctly. You may have noticed that my container is listening on port 80 while my browser is making a request on port 8081.
This is because I'm using virtualbox to virtualize my docker host, so I have to use NAT to access it from my physical host.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/b3c123ce-9a3e-449b-93ca-2d8f24032821)

![image](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/4760b7ef-0f0e-4cea-94b8-4dcccc4cefb2)

Now, the application is working properly, we can stop the containers using the docker-compose down command.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/c2f89037-e9c0-46ee-b732-5f4716b6152f)

# Private registry docker

1. The docker-compose-registry.yml file has now been created. As before, we'll launch the registry and user interface containers with the "docker-compose up -d" command.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/f9846732-0b0b-4dbf-95fb-5b345c825442)

2. Let's check that the containers have been launched:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/cf7f8410-2018-4123-b06d-c4c6349eed51)

3. We can also see with "docker log" to confirm that the UI has been launched:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/a25b7c39-f7e6-49d9-83bb-575cfd419489)

4. Let's check from a browser that the UI is accessible:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/bc71c870-a0a4-49c9-82c2-72b115e93f61)

5. We can now push our images into the registry. First, we need to consult the list of images with the "docker images" command to find out which image we're going to push so that we can tag it.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/4fb8f53b-09cc-4f58-a8cc-2e3e6de68271)

6. Then tag the images like this:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/d5d59d36-bf68-450f-8acc-b8d60d111ce0)

7. Let's check that the images have been tagged:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/6b001a45-a397-4982-8388-75dc980f37a0)

We can see that image names are now prefixed with "localhost:5000".

8. We can now push images via docker push like this. We can see here that I already have some of the image's layers in the register, as I'd already done some testing.

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/dfc85b99-f8ee-4f09-9266-d0b96a062e50)

9. Now we can see from the browser that the images have been pushed:

![image](https://github.com/rabinauget/mini-projet-docker/assets/61904489/edab2823-5c80-42eb-a83e-96ffde11a459)

# Conclusion

This project gave me a better understanding of microservice infrastructure, and deepened my technical knowledge of docker.
Configuring the Dockerfile, docker-compose.yml, images, volumes and networks, as well as the various diagnostic commands, enabled me to discover all the layers that make up Docker. 
I'm now in a better position to contribute to the improvement of containerization processes within my team.















