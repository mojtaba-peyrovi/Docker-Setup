#### How to setup Docker:

##### VirtualMachine + Docker toolbox.
after we install toolbox, there will be a terminal available on our computer called Docker Quickstart Terminal.
We need to run it. then we can run these commands:
1- docker images  => shows all images we made.
2- docker run <image_name_from_website>

3- in order to run a jupyter notebook inside a docker container, we should say this:
docker run -d -p 8888:8888 jupyter/scipy-notebook
4- list of all docker containers:
[List](https://hub.docker.com/search/?type=image)
5- full instruction to run Ducker app:
https://docs.docker.com/get-started/part2/
6- build the image from the app: docker build --tag=friendlyhello   -t is the shorter version of --tag.

__SO IMPORTANT:__ when we want to create the image naem, we need to add Doker id in the beginning. like this:  docker build -t mpeyrovi/feiendlyhello. if we dont do it, the pushing doesn't work.
7- docker system prune:   removes all images, containers, volumes and networks that are not connected anywhere.
 or
docker images -f dangling=true   it does the same thing as no 8.
8- docker rmi <Image_name>   removes the image.
9- to run the app go to this link:  http://192.168.99.100:4000/ to get this ip we can run this:
```
docker-machine ip
```
10- docker container ls  =>  shows all running docker containers.
11- container stop <container_name_or_id>   will stop the container.
12- to login to docker:   docker login  we can't use email, only ID. mine is (mpeyrovi)
13 - tagging the local repository and match with the online repository:
	docker tag <local_image>:tag <docker-repository-name>:tag
14- after tagging, docker image ls shows the online one too.

15- I made this: docker tag mpeyrovi/friendlyhello mpeyrovi/second-try:part2 and worked. I didn't mention any tag name for the local image.

16- IMPORTANT: when you create the local image add docker id behind it. example: docker build /mpeyrovi/friendlyhello
