# eval-devops

## Introduction
We created a Docker image that we put into a Github Container Registry. 
There is also a Ansible script we used to pull the image from this Container Registry.

## Used technologies

* Docker 
* Ansible 
* [Github Container Registry](https://ghcr.io)

### Ansible
Ansible is a way to automate apps and IT infrastructure.  It is used for continuous delivery of software code by taking advantage of an “infrastructure as code” approach.

Keyword : Application Deployment, Configuration Management, Continuous Delivery.

### Docker
Docker is a software platform that allows you to build, test, and deploy applications quickly. Docker packages software into standardized units called containers that have everything the software needs to run including libraries, system tools, code, and runtime.

### Github Packages (Registry)
GitHub Packages is a platform for hosting and managing packages, including containers and other dependencies..



## Install Docker on Linux

Go to this page and follow the instructions :
https://docs.docker.com/engine/install/ubuntu/

## Start Docker Daemon 
Use the following command to run the Docker Daemon :
`sudo systemctl start docker`

If this command does not work, use this :
`service docker start`



## Create & Build docker image
Create the docker image
```dockerfile
FROM nginx
COPY ./* /usr/share/nginx/html

EXPOSE 80

CMD ["nginx","-g","daemon off;"]
```

Build the image : `docker build --tag camioned-front .`

Test the image : `docker run -p 80:80 camioned-front`

## Send the image to registry
Requirement : github classic token with package W/R rights

Login to the github registry with the token : 
`docker login ghcr.io --username github-account`

Check the image id of the project : `docker images`

Use the following command to tag the Docker image : `docker tag image-id ghcr.io/github-account/camioned-front:lastest`


Then, push the image to the registry :
`docker push ghcr.io/github-account/camioned-front:lastest`

## Run the playbook

You must have ansible-playbook installed on your machine.
To do that, you can use this command (with pip installed): 

`pip install ansible`

All you have to do is run the following command : 

`ansible-playbook playbook.yml`

## Conclusion

Despite a problem encountered when retrieving our docker hosted on the Container Registery so that it could be deployed by Ansible, we learned, thanks to this mini-project, to generate and upload a docker image on Github Container Registery which serves as a container host. In a second step, we were able to discover how Ansible works by writing a Playbook.yml script. 
