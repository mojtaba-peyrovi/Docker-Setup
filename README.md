#### How to setup Docker:
- when we want to run a docker image if we just say docker run <image_name> it immediately runs it and stops it. In order to have it work, we need to add the following tags:
```
docker run -it <image_name>
```
"-it" means interactive. (we can also say -i -t). when we use it in windows we need to add "winpty" in the begining. like: winpty docker run ...

- to see what containers are running we say:
```
docker ps   or docker-compose ps
```

- to stop/remove all docker containers:
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```

##### for jupyter:
I ran this in docker terminal and it worked:
```
docker run -it -p 8887:8888 jupyter/minimal-notebook
```

##### VirtualMachine + Docker toolbox.
after we install toolbox, there will be a terminal available on our computer called Docker Quickstart Terminal.
We need to run it. then we can run these commands:
1- docker images ls  => shows all images we made.
2- docker run <image_name_from_website>

3- in order to run a jupyter notebook inside a docker container, we should say this:
```
docker run -d -p 8888:8888 jupyter/scipy-notebook
```
4- list of all docker containers:
[List](https://hub.docker.com/search/?type=image)
5- full instruction to run Ducker app part2:
##### part 2:
https://docs.docker.com/get-started/part2/
6- build the image from the app:
```
docker build --tag=friendlyhello   -t is the shorter version of --tag.
```
__SO IMPORTANT:__ when we want to create the image naem, we need to add Doker id in the beginning. like this:  docker build -t mpeyrovi/feiendlyhello. if we dont do it, the pushing doesn't work.
7-
```
docker system prune:   removes all images, containers, volumes and networks that are not connected anywhere.
or
docker images -f dangling=true

```
8-To remove an image.
```
docker rmi <Image_name>  
```

9- to run the app go to this link:  http://192.168.99.100:4000/ to get this ip we can run this:
```
docker-machine ip
```
10- to show all running docker containers.
```
docker container ls
```
11- to stop a container.
```
 container stop <container_name_or_id>
```
12- to login to docker:   
```
docker login
```
we can't use email, only ID. mine is (mpeyrovi)
13 - tagging the local repository and match with the online repository:
```
	docker tag <local_image>:tag <docker-repository-name>:tag
```
14- after tagging, "docker image ls" shows the online repositry in the list too.

15- I made this:
```
docker tag mpeyrovi/friendlyhello mpeyrovi/second-try:part2
```
 and worked. I didn't mention any tag name for the local image.

16- IMPORTANT: when you create the local image add docker id behind it. example: docker build /mpeyrovi/friendlyhello
__Conclusion:__ From now on, you can use docker run and run your app on any machine with this command:
```
docker run -p 4000:80 username/repository:tag
```

If the image isn’t available locally on the machine, Docker pulls it from the repository.

##### part 3:
https://docs.docker.com/get-started/part3/
1- first we make a yaml file called docker-compose.yml
and we copy the code from the link above.
##### We are dealing with Services in part 3
2- then we need to run this:  
```
docker swarm init --advertise-addr 192.168.99.100
```
If we don't do this, later we get this error: “this node is not a swarm manager.” Explanation in part 4
Now the swarm is being initialized.
(If an error came to say the node is already part of a swarm we can use docker swarm leave then run init again)
3-  here is time to have a name for the app:
```
docker stack deploy -c docker-compose.yml getstartedlab
```
just called it getstartedlab.
by running this, we make 5 services, becuase yml file said so.
4- we can see the services by running this:
```
docker service ls
```
#### A single container running in a service is called a task.
Tasks are given unique IDs that numerically increment, up to the number of replicas you defined in docker-compose.yml. List the tasks for your service:
```
docker service ps getstartedlab_web
```
The tasks are shown as containers. when we list all containers.
also we can say :
```
docker container ls -q
```
which shows all id's for containers.
5- we can scale up the app by simply adding as many replicas as we want at the yml file. then we run the deploy stack command and it will add more tasks.
6- in order to take down the app:
```
docker stack rm getstartedlab
```
7- take down the swarm:
```
docker swarm leave --force
```
#### part 4:
Here in part 4, you deploy this application onto a cluster, running it on multiple machines. Multi-container, multi-machine applications are made possible by joining multiple machines into a “Dockerized” cluster called a swarm.
