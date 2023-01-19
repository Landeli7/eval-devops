# eval-devops

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

```dockerfile
FROM nginx
COPY ./* /usr/share/nginx/html

EXPOSE 80

CMD ["nginx","-g","daemon off;"]
```


## Build docker image

Build the image : `docker build --tag camioned-front .`

Test the image : `docker run -p 80:80 camioned-front`

## Send the image to registry
Requirement : github token

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