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

![docker build](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/cdeccc79-fddd-4091-a90a-52d9e5781a0a)

4. We're now going to start the docker container from the image we've just created on port 5000:

![Capture d'écran 2024-05-10 194754](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/1abd3c99-71f3-45f0-8a15-b751178ead18)

5. Let's check that the container has been launched:

![docker ps after docker run Dockerfile](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/e2804206-eae5-4d42-8ea3-f4d43787c60a)

6. Now, let's confirm that the API is working. But first, we need to change the IP of the url on line 29 of website/index.php so that it points to to localhost.
   Otherwise, our request will return an error.

![Capture d'écran 2024-05-10 200516](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/a443084a-3d90-4fc1-9e70-b7204ffefdb6)

7. We can make a request to the container, specifying the user name and password supplied by the development team.

![curl after docker run](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/ab72302d-299c-48cf-be01-d7a09151e130)

8. We can now move on to creating the docker compose file to deploy the API and Frontend. To start afresh, we'll delete the container we've created.

Note that we can remove containers or images easily by indicating only the first three characters of the ID.

![Capture d'écran 2024-05-10 195835](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/7f1abac3-be94-4166-8d52-7c286a619517)

![Capture d'écran 2024-05-10 201515](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/a10c0a19-d650-44e3-a6a6-240c697d4739)

Unfortunately here, I have two different tags of the image, that's why it displays that the image is untagged. I can't delete it outright because I'm on a limited connection.
And I can't completely delete the image in question because it's still going to be useful for the rest of the project.

# Infrastructure As Code

1. After deleting the container and image, we created the docker-compose.yml file (you'll find it in the repository), which we'll use to deploy/manage/bind together the frontend in an API-dependent way.
Let's launch it:

![docker-compose up API et frontend](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/dce082ed-c24e-467b-8bb1-7699d122a53e)

Here we can see that the API and Frontend containers have been created, as well as the mini-project_pozos_network we declared in the docker-compose file.
The -d option is used to launch containers in the background.

2. Let's check that the containers have been launched using the "docker ps" command:

![Capture d'écran 2024-05-10 202653](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/55cba70d-e460-4097-a526-9184656176d8)

We can see that containers are running and the frontend is listening on port 80.

3. We can now run a test via a browser. Note that a modification has also been made to the index.php file so that its IP points to the name of the API container in the docker-compose.
So, whatever the IP of the container, the API will always be accessible.

![image](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/45d352e3-1ea5-4aa4-924b-74a3d35d69a9)

4. The application works correctly. You may have noticed that my container is listening on port 80 while my browser is making a request on port 8081.
This is because I'm using virtualbox to virtualize my docker host, so I have to use NAT to access it from my physical host.

![image](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/4760b7ef-0f0e-4cea-94b8-4dcccc4cefb2)

Now, the application is working properly, we can stop the containers using the docker-compose down command.

![Capture d'écran 2024-05-10 203109](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/1d11fb88-34e5-4ff7-bc5a-0fd6c77eac7f)

# Private registry docker

1. The docker-compose-registry.yml file has now been created. As before, we'll launch the registry and user interface containers with the "docker-compose up -d" command.

![docker-compose up registry et ui](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/11d155d1-6dc1-4ef7-938d-96e43e35208f)

2. Let's check that the containers have been launched:

![docker-compse ps after docker compose up regitry et ui](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/e7995c70-0260-4cfc-aa3f-af74a450bf31)

3. We can also see with "docker log" to confirm that the UI has been launched:

![docker log ui](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/b7363bc6-8a0d-425d-b8ad-52e9176ad547)

4. Let's check from a browser that the UI is accessible:

![image](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/97e4e3fb-b054-42d1-aa0e-fae9ff7c9fe1)

5. We can now push our images into the registry. First, we need to consult the list of images with the "docker images" command to find out which image we're going to push so that we can tag it.

![Capture d'écran 2024-05-10 210000](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/7bbcdc76-d97b-42a4-bfcd-b1716ddc2027)

6. Then tag the images like this:

![Capture d'écran 2024-05-10 210241](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/028655f5-9506-4fc9-8114-43b5fcd41350)

7. Let's check that the images have been tagged:

![Capture d'écran 2024-05-10 210324](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/e7a97524-2bc5-4714-b516-8502852125e1)

We can see that image names are now prefixed with "localhost:5000".

8. We can now push images via docker push like this:

![docker push](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/2c2eab38-cbc1-43ab-bf50-d114092c9745)

9. Now we can see from the browser that the images have been pushed:

![Browser access after docker compose up registry ](https://github.com/RabinaAuget/mini-projet-docker/assets/61904489/af5ca790-b95d-48b2-bac8-668b6abb0a71)

# Conclusion

This project gave me a better understanding of microservice infrastructure, and deepened my technical knowledge of docker.
Configuring the Dockerfile, docker-compose.yml, images, volumes and networks, as well as the various diagnostic commands, enabled me to discover all the layers that make up Docker. 
I'm now in a better position to contribute to the improvement of containerization processes within my team.















