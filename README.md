# eval-devops

## Used technologies

* Docker
* Ansible
* [Github Container Registry](https://ghcr.io)

## Install Docker on Linux

Go to this page and follow the instructions :
https://docs.docker.com/engine/install/ubuntu/

## Start Docker Daemon 
Use the following command to run the Docker Daemon :
`sudo systemctl start docker`

If this command does not work, use this :
`service docker start`

## Build docker image

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
