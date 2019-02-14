#### Docker composer:

- It is a tool for defining and running multi-container applications.
- we use docker-compose.yml file to configure application services.
- we can start all services with a single command: docker compose up
- we can stop all services with a single command: docker compose down
- we can scale up services whenever required

##### step 1:
for windows docker composer comes with docker already afer we install docker.
- to check if docker composer is installed we can say:
```
docker-compose -v   or docker-compose version   or docker-compose --version
```
#### step 2:
create docker compose file at any location on our system. the name of the file should be docker-compose.yml
I made a folder called web-app-docker-example and inside it made the docker-compose.yml file.

#### step 3:
Checking the validity of the file by this command: (navigate to the folder where the yml files exists)
```
docker-compose config
```
sometimes the version we give to our docker-compose is not compatible with the docker version we already have.
[here](https://docs.docker.com/compose/compose-file/) is a link that shows the compatibility matrix.
First we put version: '1'  in yml file but it didn't work. Now we change it to 3 and it works.

Anytime the config command returns the contents of the yml file it means it works.

#### step 4:
Run docker-compose.yml file using this command:
```
docker-compose up -d
```
when we run this command, it makes the app structure and -d means make it in detached mode.
#### step 5:
when we want to have the containers down we just say:
```
docker-compose down
```
Now if we expose the app to the port 9090 according to yml file, we can open the application at this link:
http://192.168.99.100:9090/

#### step 6:
to scale up the app. we should use --scale flag when we are having compose up and after that we specify which service and how many instances we want:
```
docker compose up -d --scale datbase=4
```

__IMPORTANT:__ In order to see the containers running in a specific folder, not the whole machine, we navigate to the folder then:
```
docker-compose ps
```
