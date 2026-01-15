# How to run?

conda create -n test python=3.11 -y

conda activate test

pip install -r requirements.txt


## Docker Test

docker pull hello-world

docker run hello-world


```bash
docker ps                                   # See a list of all running containers
docker ps -a                                # See a list of all containers, even the ones not running
docker rm <hash>                            # Remove the specified container from this machine
docker rm $(docker ps -a -q)                # Remove all containers from this machine
docker images -a                            # Show all images on this machine
docker rmi <imagename>                      # Remove the specified image from this machine
docker rmi $(docker images -q)              # Remove all images from this machine
```


## Docker Custom image

docker build -t entpriyansh/mycalapp:latest . '

<!-- ALWAYS REMEMBER -->
<!-- docker build -t <username>/mycalapp:latest  -->

docker run -p 6969:8080 entpriyansh/mycalapp:latest

docker run -d -p 8080:8080 entpriyansh/mycalapp:latest 



## Push to Docker Hub:

1. docker login  
2. docker push entpriyansh/mycalapp:latest     