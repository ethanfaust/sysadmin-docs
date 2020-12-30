# Docker

## Setup
```
sudo yum install -y docker-io
sudo systemctl start docker
sudo systemctl enable docker
```

## Usage
```
docker pull fedora
```

```
sudo docker run -i -t fedora /bin/bash
sudo docker run -i -t fedora /bin/echo 'Hello, world!'
```

* run starts a new instance of the named container

```
sudo docker ps -a
```

* ps lists containers (-a includes "all", even stopped containers)

```
$ sudo docker run -i -t fedora /bin/bash
# make some changes to filesystem and then exit
$ sudo docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
b7f7e61cb244        fedora:latest       /bin/bash           29 seconds ago      Exited (0) 8 seconds ago                       sharp_lovelace
$ sudo docker commit -m 'added foo' -a 'Ethan Faust' b7f7e61cb244 mine/foo
227298528a87b8259ad7c161a739295407c71f28754098898d96f31792fca754
```

```
# list images
sudo docker images
 
# remove image
sudo docker rmi <image id>
```

## Dockerfile
* This creates a build recipe 'Dockerfile'
    * Can copy files from local directory
    * Can execute commands inside image
    * And more! See [Documentation](https://docs.docker.com/reference/builder/)

```
$ cat > Dockerfile << EOF
FROM fedora
MAINTAINER Ethan Faust <ethan@faust.us>
RUN echo 'my data' > /home/foo
COPY ./test /home/test
EOF
$ cat > ./test << EOF
success
EOF
$ sudo docker build -t "mine/build" .
```

## References
* [Minimal Docker Container](http://dustymabe.com/2014/07/07/creating-your-own-minimal-docker-image-in-fedora/)
* [Docker + broken init system](http://phusion.github.io/baseimage-docker/#intro)
