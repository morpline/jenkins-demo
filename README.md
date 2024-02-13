# jenkins-demo
 
I followed the steps from: https://www.jenkins.io/doc/book/installing/docker/

Here are the commands I ran from the tutorial formatted in a way that will actually run.

(They are out of order, the install took a couple tries.)

## Install

Open terminal in root folder.

Run commands 3, 4, 2, and 5 in that order.

Copy the password from the terminal.

Go to localhost:8080 and input it there.

Click "Install Suggested Plugins"

Create user, if wanted.

Choose a port. I chose 7340, but you can choose whatever you want.

## Command 1

docker run --name jenkins-docker --rm --detach --privileged --network jenkins --network-alias docker --env DOCKER_TLS_CERTDIR=/certs --volume jenkins-docker-certs:/certs/client --volume jenkins-data:/var/jenkins_home --publish 2376:2376 docker:dind

## Command 2

docker run --name jenkins-blueocean --restart=on-failure --detach --network jenkins --env DOCKER_HOST=tcp://docker:2376 --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 --volume jenkins-data:/varjenkins_home --volume jenkins-docker-certs:/certsclient:ro --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.426.3-1

## Command 3

docker run  --name jenkins-docker  --rm  --detach  --privileged  --network jenkins  --network-alias docker  --env DOCKER_TLS_CERTDIR=/certs  --volume jenkins-docker-certs:/certs/client  --volume jenkins-data:/var/jenkins_home  --publish 2376:2376  docker:dind  --storage-driver overlay2

## Command 4

docker build -t myjenkins-blueocean:2.426.3-1 .

## Command 5

docker logs jenkins-blueocean