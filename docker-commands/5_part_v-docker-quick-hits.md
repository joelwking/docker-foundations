# Part V - Docker Quick Hits

### Docker Exec

Show the current working directory of your Docker Container:

```bash
docker exec -it my_cont pwd
```



List all files in the working directory of your Docker Container:

```bash
docker exec -it my_cont ls -la
```



View the contents of the system release information file for your Docker Container:

```bash
docker exec -it my_cont sh -c "cat /etc/*-release"
```



Run the Python script in your Docker Container:

```bash
docker exec -it my_cont python my_script.py
```



------



### Docker Networks

Display a list of your Docker Networks:

```bash
docker network list
```



Display details for the Docker ***bridge*** Network and review the default ***subnet***.

```bash
docker inspect network bridge
```



Create a new Docker Network based on the ***bridge*** Network Driver:

```bash
docker network create --driver bridge my_net
```



Display a list of your Docker Networks and observe the new Network, ***my_net***.

```bash
docker network list
```



Display details for the Docker ***my_net*** Network and review the ***subnet***:

```bash
docker inspect network my_net
```



Create two new Containers in ***detached*** mode (<font color="red">***-d*** </font>flag) and attach both to the ***my_net*** Network:

```bash
# Syntax option #1
docker container run -itd --net my_net --name my_cont1 my_image
docker container run -itd --network my_net --name my_cont2 my_image

# Syntax option #2
docker run -itd --net my_net --name my_cont1 my_image
docker run -itd --network my_net --name my_cont2 my_image
```

**The <font color="red">*--net*</font> and <font color="red">*--network*</font> flags are interchangeable.**



Display a list of your Docker Containers with either of these commands:

```bash
docker container ls -a
docker ps -a
```



Show the interface details for ***eth0*** on the Container ***my_cont1*** and locate the ***IP address*** (<font color="red">***inet_addr***</font>):

```bash
docker exec -it my_cont1 ifconfig eth0
```



Show the interface details for ***eth0*** on the Container ***my_cont2*** and locate the ***IP address*** (<font color="red">***inet_addr***</font>):

```bash
docker exec -it my_cont2 ifconfig eth0
```



Ping Container ***my_cont2*** from ***my_cont1*** and notice that Docker ***Auto DNS*** resolves the correct IP address:

```bash
docker exec -it my_cont1 ping -c 4 my_cont2
```



Ping Container ***my_cont1*** from ***my_cont2*** and notice that Docker ***Auto DNS*** resolves the correct IP address:

```bash
docker exec -it my_cont2 ping -c 4 my_cont1
```



------



### Docker Compose

Display a list of your Docker Containers with either of these commands:

```bash
docker container ls -a
docker ps -a
```



Build and deploy the web application with Docker Compose:

```bash
docker-compose -d up
```



Display a list of your Docker Containers and observe the ***five new*** Docker Containers with either of these commands:

```bash
docker container ls -a
docker ps -a
```



Test HTTP connectivity to each of the front-end web servers and observe the ***Hello World*** response:

```bash
curl http://localhost:5001
curl http://localhost:5002
curl http://localhost:5003
```



Stop and remove the web application with Docker Compose:

```bash
docker-compose -d down
```



Display a list of your Docker Containers and observe the web application Containers no longer exist:

```bash
docker container ls -a
```



------



### Cleaning Up

Show a summary of Docker storage consumption:

```bash
docker system df
```



Show verbose details of Docker storage consumption:

```bash
docker system df -v
```



Stop all running Docker Containers with either of these commands:

```bash
docker container stop $(docker container ls -q)
docker stop $(docker container ls -q)
```

**The <font color="red">*-q*</font> flag indicates <font color="red">*quiet mode*</font> wich limits the output to the Container ID only.**



Remove all ***stopped*** Containers:

```bash
docker container prune
```



Remove all ***dangling*** Images:

```bash
docker image prune
```



Remove all:

- Dangling Images
- Stopped Containers
- Unused Networks
- Build cache

```bash
docker system prune
```



Remove all of the above ***plus*** all:

- Unused Volumes

```bash
docker system prune --volumes
```



Remove all ***dangling*** and ***unused*** Images - those with no associated Containers:

```bash
dockr image prune -a
```

