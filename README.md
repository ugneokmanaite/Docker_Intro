# Intro to Docker! 

![image](https://bdlguu0syu1idj5d2b4m53mv-wpengine.netdna-ssl.com/wp-content/uploads/2019/01/KubernetesDockerpic1.png)

## What is containersization?

## What is Docker?
Tool designed to make it easier to create, deploy and run applications using containers

## What are containers?
Allow developer to package up an application with all te required parts e.g. libraries and reploy it as one package

## Docker VS Vagrant

###Vagrant 
- Needed to spin up a virtual machine to enable identical environment to the production environments for everyone
- Ensures application can be ran
- VM requires provisioning script to run all the required configurations to provision the machine
- Project code is inserted into environments

### Docker 
- Runs off containers
- Docker file runs docker image which includes all project code (complete & executable version of application)
- This image is designed to sit at the top of the machine (container)--> you can run as many containers as you like
- Docker builds your environment and it can be run anywhere 
- Then this image is pushed into DockerHub and now any machine can run your image! 
- Lightweight in comparison to VMs --> it shares the memory of OS then creating an entire virtual env

## What is a container?


syntax for this is 
`docker run username/repo_name`

## Some Commands!!!

```
docker ps     > checks for running containers

docker ps -a  > shows all the running & exited containers

docker pull   > pull images from the docker repository

docker run -it d <image name> > create a contrainer from an image

docker exec -it <container id> bash > to access the running container

docker stop      > stops a running container

docker kill      > kills container by stopping execution. stop gives time to shut down gracefully

docker commit <container id><username/imagename>       > creates new image of an edited container on local system

docker login     > login into the docker hub repo

docker push <username/imagename>    > push image to the docker hub repo 

docker images     > lists all locally stored images

docker rm <container id>  > delete a stopped container

docker rmi <image_is>   > delete an image from local storage

docker build <path to dockerfile>  > build an image from a specified docker file

```
## Adding winpty docker to ENV variables
- Allows windows users to easily enter docker containers 
- Add this into ENV variables via git bash or system if needed
```
alias docker="winpty docker"
```

## Entering container
```
docker exec -it container_id sh
```
## Port mapping 
- With the below command we are running nginx on our local host port 90

```docker run -p 80:80 nginx```

- With the command below we have changed our nginx so that is shows on port 99 instead of port 80

```docker run -p 99:80 nginx```


# How To Use the Official NGINX Docker Image 

documentation : https://www.docker.com/blog/how-to-use-the-official-nginx-docker-image/

https://hub.docker.com/_/nginx

## Step 1: docker ps
- Ensure any other images running on required port have been stopped

## Step 2: Create a directory named site-content 
- Create this inside your os 

## Step 3: Add index.html file
- This will be the html you will want to use instead of default inside `usr/share/nginx/html`

## Step 4: In same directory create a Dockerfile
```
FROM nginx:latest
COPY ./index.html /usr/share/nginx/html/index.html
```
Used to generate a new image that includes the necessary content

FROM = allows us to build custom image by using the base image. This will pull nginx:latest image to our local machine and then build our custom image on top of it 

COPY = copy the new index.html file into the location of default one. THIS OVERWRITES IT

## Step 5: Build image
``` docker build -t testing-nginx .```

## Step 6: Run the image 
```
docker run -d -p 80:80 testing-nginx 
```

## Step 7: Test in browser 
`http://localhost/` in the browser should display contents of newly added index.html

## Step 8: Tag the image to a repo
```
docker tag 21013cfc729e okmanaiu/eng67.ugne.nginx:testing_own_index
```
`docker tag <image id> <username/reponame:version_name>`

## Step 9: Push to repo

```
docker push okmanaiu/eng67.ugne.nginx
```







